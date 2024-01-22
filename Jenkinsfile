rary('library-demo') _
pipeline {
    agent {label 'java'}
    stages {
        stage('Checkout') {
            steps {
                script {
                    sh  'rm -rf bus_booking'
                    sh  'git clone https://github.com/yatheesh2328/bus_booking.git'
                }
            }
        }
        stage('build') {
            steps {
                script {
                    sh 'mvn clean install'
                }
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
