@Library("myLib") _

pipeline {
    agent { label 'slave01'}
    stages {
        stage('checkout') {
            steps {
                script {
                myFunction.remove('Bus-sonar-lib')
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
                       sonarScan()
				}
             }
			}
}
}
// post {
//     failure {
//         mail to: 'jagruthisbhandare@gmail.com',
//              subject: "Failed Pipeline: Hello-world-war",
//              body: "Something is wrong with https://github.com/Jagruthi111/hello-world-war"
//     }
}
}
