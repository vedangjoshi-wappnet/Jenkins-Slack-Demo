pipeline {
    agent any

    stages {
        stage('Notify Start') {
            steps {
                withCredentials([string(credentialsId: 'Slack-webhook', variable: 'SLACK_WEBHOOK')]) {
                    sh """
                    curl -X POST -H 'Content-type: application/json' \
                    --data '{"text":"🚀 Build started for ${env.JOB_NAME}"}' \
                    $SLACK_WEBHOOK
                    """
                }
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
            withCredentials([string(credentialsId: 'Slack-webhook', variable: 'SLACK_WEBHOOK')]) {
                sh """
                curl -X POST -H 'Content-type: application/json' \
                --data '{"text":"✅ Build SUCCESS: ${env.JOB_NAME}"}' \
                $SLACK_WEBHOOK
                """
            }
        }
        failure {
            withCredentials([string(credentialsId: 'Slack-webhook', variable: 'SLACK_WEBHOOK')]) {
                sh """
                curl -X POST -H 'Content-type: application/json' \
                --data '{"text":"❌ Build FAILED: ${env.JOB_NAME}"}' \
                $SLACK_WEBHOOK
                """
            }
        }
    }
}