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
                sh '''
                    export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
                    export PATH=$JAVA_HOME/bin:$PATH

                    java -version
                    javac -version
                    mvn -version
                    mvn clean install
                '''
            }
        }

        stage('Upload to Artifactory') {
            steps {
                 usernamePassword([
                credentialsId: 'jfrog',
                usernameVariable: 'JFROG_USER',
                passwordVariable: 'JFROG_PASS'
                 )
            ]) {
                    sh '''
                        export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
                        export PATH=$JAVA_HOME/bin:$PATH

                        mvn deploy \
                          -DskipTests \
                          -Dusername=$ART_USER \
                          -Dpassword=$ART_PASS
                    '''
                }
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
