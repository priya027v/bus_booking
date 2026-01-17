pipeline {
    agent { label 'slave2' }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Application') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
                sh 'mvn clean install'
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                    nohup mvn spring-boot:run > app.log 2>&1 &
                    sleep 15
                '''
            }
        }
    }
}
