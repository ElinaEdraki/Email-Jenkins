pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                // Run some test command
                bat 'echo Running tests...'
                // Copy full Jenkins console log for this build
                bat "copy %WORKSPACE%\\..\\${env.JOB_NAME}@tmp\\logs\\${env.BUILD_NUMBER}.log test.log"
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
                // Run some scan command
                bat 'echo Running security scan...'
                // Copy full Jenkins console log for this build
                bat "copy %WORKSPACE%\\..\\${env.JOB_NAME}@tmp\\logs\\${env.BUILD_NUMBER}.log scan.log"
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
