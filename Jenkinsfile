pipeline{
    
    agent any

	environment {
		registry = "424377644605.dkr.ecr.eu-west-2.amazonaws.com/f2ride-dev/nodeapp"
		dockerImage = ''
  	}
   
    stages { 

		stage('Static Code analysis') {
       
			environment {
			scannerHome = tool 'f2ride-sonar-scanner'
			}

			steps {

				withSonarQubeEnv('Sonarqube-server') {
					sh "${scannerHome}/bin/sonar-scanner -Dsonar.login='7e19dab3495025af989d6cad00d0fdc166e734b9' -Dsonar.projectKey=f2ride-web -Dsonar.sources='.'"
				}

			}
    	} 
	    
stage("Quality Gate") {

       

        steps {
          timeout(time: 2, unit: 'MINUTES') {
            waitForQualityGate(webhookSecretId: '1234') 
          }
        }
    }
    
	    
		stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        
       stage('Build image') {
		steps{
			script {
			dockerImage = docker.build ('f2ride-dev/nodeapp')
			}
     	 }
   		}

		stage('Deploy Image') {
		steps{
			script {
			docker.withRegistry( 'https://424377644605.dkr.ecr.eu-west-2.amazonaws.com', 'ecr:eu-west-2:prasanna-dev-ecr' ) {
				docker.image('f2ride-dev/nodeapp').push('latest')
			}
			}
		}
		}
        
    }
}
