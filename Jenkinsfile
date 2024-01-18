
pipeline {
    agent {
        label 'slave01'
    }

    environment {
        MAVEN_HOME = tool 'Maven'
        //SPRING_PROFILES_ACTIVE = 'local'  
    }


    stages {
        stage('checkout') {
            steps {
                sh 'rm -rf bus_booking'
                sh 'git clone https://github.com/Jagruthi111/bus_booking.git'
            }
        }

        stage('build') {
            steps {
                script {
                     sh "${MAVEN_HOME}/bin/mvn clean package"
                }
            }
        }

        stage('Run JAR') {
            steps {
                script {
                    sh "java -jar target/bus-booking-app-1.0-SNAPSHOT.jar&"
		    sleep 30
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
			sh "ssh root@172.31.2.55"
                    sh "scp target/bus-booking-app-1.0-SNAPSHOT.jar root@172.31.2.55:/opt/apache-tomcat-8.5.98/webapps/"
                }
            }
        }
    }

}
