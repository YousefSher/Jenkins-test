pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // Checkout code to make git info available
                checkout scm
                script {
                    // Get latest commit info
                    def commitHash = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
                    def author = sh(script: "git log -1 --pretty=format:'%an'", returnStdout: true).trim()
                    def message = sh(script: "git log -1 --pretty=format:'%s'", returnStdout: true).trim()
                    
                    // Save to environment for post section
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
