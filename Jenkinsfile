pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Chaitanya932000/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0' // Continue even if tests fail
            }
        }
        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }
        stage('Send Email Notification') {
            steps {
                script {
                    emailext (
                        subject: "Build ${env.JOB_NAME} #${env.BUILD_NUMBER} - ${currentBuild.currentResult}",
                        body: """<p>Build result: <b>${currentBuild.currentResult}</b></p>
                                 <p>Job: ${env.JOB_NAME}</p>
                                 <p>Build number: ${env.BUILD_NUMBER}</p>
                                 <p>Build URL: <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></p>
                                 <p>Check the console output for details.</p>""",
                        to: 'chaitanyapatil932000@gmail.com',
                        mimeType: 'text/html'
                    )
                }
            }
        }
    }
}
