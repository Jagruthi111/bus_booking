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
stage('Deploy to JFrog Artifactory') {
            steps {
                script {
                    rtServer(
                        id: "Artifact",
                        url: "http://3.110.221.84:8081/artifactory",
                        username: "jagruthi",
                        password: "Jagruthi11"
                    )
                }
            }
        }

        stage('Upload') {
            steps {
                script {
		// For my  undertanding rtUpload is a part of jFrog Artifactory plugin to upload artifacts to artifacts repo
                    rtUpload (
                        serverId: 'Artifact',
                        spec: '''{
                            "files": [
                                {
                                    "pattern": "target/*.jar",
                                    "target": "libs-release-local/"
                                }
                            ]
                        }'''
                    )
                }
            }
        }

        stage('Publish build info') {
            steps {
                script {
		    // For my understanding to publish build info
                    rtPublishBuildInfo serverId: "Artifact"
                }
            }
        }
    }



