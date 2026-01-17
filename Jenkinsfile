pipeline {
    agent {
        label 'king'
    }

    environment {
        TOMCAT_HOST = '16.171.40.186'
        TOMCAT_USER = 'root'
        TOMCAT_DIR = '/opt/tomcat/webapps'
        JAR_FILE = 'bus-booking-app-1.0-SNAPSHOT.jar'  // Replace with the actual name of your JAR file
    }

    stages {
        stage('checkout') {
            steps {
                sh 'rm -rf bus_booking'
                sh 'git clone https://github.com/priya027v/bus_booking.git'
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
    }
}
