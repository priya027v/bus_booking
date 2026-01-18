pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                cleanWs()
                git branch: 'feature-1',
                    url: 'https://github.com/priya027v/bus_booking.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                    mvn clean install
                '''
            }
        }

        // stage('Run App (5 min)') {
        //     steps {
        //         timeout(time: 5, unit: 'MINUTES') {
        //             sh '''
        //                 java -jar target/bus-booking-app-1.0-SNAPSHOT.war
        //             '''
        //         }
        //     }
        // }

    //     stage('Publish') {
    //         steps {
    //             withCredentials([
    //                 usernamePassword(
    //                     credentialsId: 'jfrog',
    //                     usernameVariable: 'JFROG_USER',
    //                     passwordVariable: 'JFROG_API_KEY'
    //                 )
    //             ]) {
    //                 sh '''
    //                     mvn deploy
    //                 '''
    //             }
    //         }
    //     }
    // }
        stage('Publish') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'jfrog',
                        usernameVariable: 'JFROG_USER',
                        passwordVariable: 'JFROG_API_KEY'
                    )
                ]) {
                    configFileProvider([
                        configFile(
                            fileId: 'maven-settings-jfrog',
                            variable: 'MAVEN_SETTINGS'
                        )
                    ]) {
                        sh '''
                            mvn deploy -s $MAVEN_SETTINGS
                        '''
                    }
                }
            }
        }
    }
}
