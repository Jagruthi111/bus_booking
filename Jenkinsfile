pipeline {
    agent {
        label 'slave01'
    }

    // environment {
    //    TOMCAT_HOST = '172.31.2.55'
    //    TOMCAT_USER = 'root'
    //    TOMCAT_DIR = '/opt/apache-tomcat-8.5.98/webapps'
    //    JAR_FILE = 'bus-booking-app-1.0-SNAPSHOT.jar'  
    //    }

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
                    def mvnHome = tool 'Maven'
                    def mvnCMD = "${mvnHome}/bin/mvn"
                    sh "${mvnCMD} clean install"
                }
            }
        }

        stage('Run JAR') {
            steps {
                script {
                    sh "java -jar target/${JAR_FILE}"
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh "scp target/bus-booking-app-1.0-SNAPSHOT.jar root@172.31.2.55:/opt/apache-tomcat-8.5.98/webapps/"
                    sh "ssh root@172.31.2.55 'bash -s' < restart-tomcat.sh"
                }
            }
        }
    }

}
