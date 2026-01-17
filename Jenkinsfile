pipeline {
    agent { label 'slave1' }

    tools {
        jdk 'Java21.0.9'
        maven ' Maven 3.8.7'
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo 'Cloning Bus Booking repository...'
                checkout scm
            }
        }

        stage('Build Application') {
            steps {
                echo 'Building application using Maven...'
                sh 'mvn clean install'
            }
        }
    }
}
