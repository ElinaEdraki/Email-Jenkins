pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                // Run some test command
                sh 'echo "Running tests..."'
                // Copy full Jenkins console log for this build
                sh "cp \$WORKSPACE/../${env.JOB_NAME}@tmp/logs/${env.BUILD_NUMBER}.log test.log"
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
                sh 'echo "Running security scan..."'
                // Copy full Jenkins console log for this build
                sh "cp \$WORKSPACE/../${env.JOB_NAME}@tmp/logs/${env.BUILD_NUMBER}.log scan.log"
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
