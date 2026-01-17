pipeline {
    agent { label 'slave1' }

    tools {
        jdk 'Java11'
        maven 'Maven3'
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
