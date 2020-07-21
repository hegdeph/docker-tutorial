pipeline{
    
    agent any

	stages{
	stage('Static Code analysis') {
       
        environment {
          scannerHome = tool 'f2ride-sonar-scanner'
        }

        steps {

            withSonarQubeEnv('Sonarqube-server') {
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.login='1b460da1a67ec5961f38bd92baed13b957b1252f' -Dsonar.projectKey=f2ride-web -Dsonar.sources='./*'"
            }

        }
    } 
	}
}
