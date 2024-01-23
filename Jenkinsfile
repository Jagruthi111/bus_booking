@Library("myLib") _
pipeline {
    agent { label 'slave01'}
    stages {
        stage('checkout') {
            steps {
                script {
                myFunction.remove('bus_booking')
                myFunction.clone('https://github.com/Jagruthi111/bus_booking.git')
              }  
          }
        }
        stage('build') {
            steps {
                mvnVersion()
                mavenBuild()
            }
        }
           stage('SonarQube Scan') {
               steps {
			   withSonarQubeEnv('sonar'){
				script {
                       sonar()
				}
             }
			}
           }
    }
}
