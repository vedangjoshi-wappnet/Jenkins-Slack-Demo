pipeline {
    agent any

    stages {
        stage('Notify Start') {
            steps {
                slackSend(
                    channel: "#build-logs",
                    tokenCredentialId: "slack-webhook",
                    message: "🚀 Build started for ${env.JOB_NAME}"
                )
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
            slackSend(
                channel: "#build-logs",
                tokenCredentialId: "slack-webhook",
                message: "✅ Build SUCCESS: ${env.JOB_NAME}"
            )
        }
        failure {
            slackSend(
                channel: "#build-logs",
                tokenCredentialId: "slack-webhook",
                message: "❌ Build FAILED: ${env.JOB_NAME}"
            )
        }
    }
}