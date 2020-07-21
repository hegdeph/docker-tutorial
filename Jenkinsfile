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
			dockerImage = docker.build registry + ":$BUILD_NUMBER"
			}
     	 }
   		}

		stage('Deploy Image') {
		steps{
			script {
			docker.withRegistry( '', 'Prasanna-Dev' ) {
				dockerImage.push()
			}
			}
		}
		}
        
    }
}
