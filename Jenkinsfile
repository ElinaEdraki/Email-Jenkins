pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                bat 'echo Running tests... > test.log'
            }
            post {
                always {
                    emailext(
                        to: 'elinaedraki@gmail.com',
                        subject: "Test Stage: ${currentBuild.currentResult}",
                        body: "The Test stage finished with status: ${currentBuild.currentResult}",
                        attachmentsPattern: 'test.log'
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                bat 'echo Running security scan... > scan.log'
            }
            post {
                always {
                    emailext(
                        to: 'elinaedraki@gmail.com',
                        subject: "Security Scan Stage: ${currentBuild.currentResult}",
                        body: "The Security Scan stage finished with status: ${currentBuild.currentResult}",
                        attachmentsPattern: 'scan.log'
                    )
                }
            }
        }
    }
}
