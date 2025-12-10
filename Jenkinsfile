pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                checkout scm
                script {
                    def commitHash = bat(script: "git rev-parse HEAD", returnStdout: true).trim()
                    def author = bat(script: "git log -1 --pretty=format:'%an'", returnStdout: true).trim()
                    def message = bat(script: "git log -1 --pretty=format:'%s'", returnStdout: true).trim()
                    env.LAST_COMMIT = commitHash
                    env.LAST_AUTHOR = author
                    env.LAST_MESSAGE = message
                }
            }
        }
    }
    post {
        always {
            emailext(
                to: 'yousefsmn@gmail.com',
                subject: "${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Commit: ${env.LAST_COMMIT}, made by ${env.LAST_AUTHOR}, with message: ${env.LAST_MESSAGE}"
            )
        }
    }
}
