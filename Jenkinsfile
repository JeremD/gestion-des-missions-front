pipeline {
    agent any
    tools {
        nodejs 'NodeJS 14.8'
    }
    stages {
        stage('verify') {
            steps {
                sh 'node -v'
            }
        }
        stage('build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('deploy') {
            when {
                branch 'master'
            }
            steps {
                echo "ng deploy --base-href=${GHPAGES_MISSIONS}"
            }
            post {
                failure {
                     discordSend description: "${env.GIT_URL} | ${env.GIT_COMMIT}", footer: "#${env.BUILD_NUMBER} - Failure", image: '', link: "${env.BUILD_URL}", result: 'FAILURE', thumbnail: "${env.AVATAR}", title: "${env.JOB_NAME}, ${env.GIT_BRANCH}", webhookURL: "${env.WEBHOOK_URL}"
                }
                success {
                    discordSend description: "${env.GIT_URL} | ${env.GIT_COMMIT}", footer: "#${env.BUILD_NUMBER} - Success", image: '', link: "${env.BUILD_URL}", result: 'SUCCESS', thumbnail: "${env.AVATAR}", title: "${env.JOB_NAME}", webhookURL: "${env.WEBHOOK_URL}"
                }
            }
        }
    }
}
