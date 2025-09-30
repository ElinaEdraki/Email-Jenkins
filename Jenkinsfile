pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                // Run some test command
                bat 'echo Running tests... > test.log'

                // Copy full Jenkins console log for this build into test.log
                bat "copy \"%WORKSPACE%\\..\\${env.JOB_NAME}@tmp\\logs\\${env.BUILD_NUMBER}.log\" test.log >nul"
            }
            post {
                always {
                    emailext(
                        to: 'elinaedraki@gmail.com',
                        subject: "Test Stage: ${currentBuild.currentResult}",
                        body: """The Test stage finished with status: ${currentBuild.currentResult}.
                                 Please see attached log file for details.""",
                        attachmentsPattern: 'test.log'
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                // Run some scan command
                bat 'echo Running security scan... > scan.log'

                // Copy full Jenkins console log for this build into scan.log
                bat "copy \"%WORKSPACE%\\..\\${env.JOB_NAME}@tmp\\logs\\${env.BUILD_NUMBER}.log\" scan.log >nul"
            }
            post {
                always {
                    emailext(
                        to: 'elinaedraki@gmail.com',
                        subject: "Security Scan Stage: ${currentBuild.currentResult}",
                        body: """The Security Scan stage finished with status: ${currentBuild.currentResult}.
                                 Please see attached log file for details.""",
                        attachmentsPattern: 'scan.log'
                    )
                }
            }
        }
    }
}
