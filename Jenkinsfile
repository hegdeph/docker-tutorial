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
					sh "${scannerHome}/bin/sonar-scanner -Dsonar.login='1b460da1a67ec5961f38bd92baed13b957b1252f' -Dsonar.projectKey=f2ride-web -Dsonar.sources='.'"
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
