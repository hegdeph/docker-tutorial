		 pipeline{
    
        agent any
   

    stages {
        
      
stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        
       stage('Build image') {
           
           
           steps{
               script{
                docker.build '424377644605.dkr.ecr.eu-west-2.amazonaws.com/f2ride-dev/nodeapp:latest'
               }
           }
    }
    stage('Push image') {
        
        
        
        steps {
            script{
                 docker.withRegistry('https://424377644605.dkr.ecr.eu-west-2.amazonaws.com/f2ride-dev/nodeapp', 'ecr:eu-west-2:Prasanna-Dev') 
            }
            
                {
                sh "docker push 424377644605.dkr.ecr.eu-west-2.amazonaws.com/f2ride-dev/nodeapp:latest"
                }
        }
    }
        
    }
    }
