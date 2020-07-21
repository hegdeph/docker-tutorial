pipeline{
    
    agent any

	environment {
		registry = "424377644605.dkr.ecr.eu-west-2.amazonaws.com/f2ride-dev/nodeapp"
		dockerImage = ''
  	}
   
    stages {
		stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        
       stage('Build image') {
		steps{
			script {
			dockerImage = docker.build ('nodeapp')
			}
     	 }
   		}

		stage('Deploy Image') {
		steps{
			script {
			docker.withRegistry( 'https://424377644605.dkr.ecr.eu-west-2.amazonaws.com', 'ecr:eu-west-2:prasanna-dev-ecr' ) {
				docker.image('nodeapp').push('latest')
			}
			}
		}
		}
        
    }
}
