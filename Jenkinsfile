pipeline {
    agent any

    stages {
        stage('Notify Start') {
            steps {
                slackSend(message: "🚀 Build started for ${env.JOB_NAME}")
            }
        }

        stage('Build') {
            steps {
                sh 'echo Building project...'
                sh 'sleep 60'
            }
        }
    }

    post {
        success {
            slackSend(message: "✅ Build SUCCESS: ${env.JOB_NAME}")
        }
        failure {
            slackSend(message: "❌ Build FAILED: ${env.JOB_NAME}")
        }
    }
}