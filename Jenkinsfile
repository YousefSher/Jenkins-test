pipeline {
    agent any
    triggers {
        githubPush()
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
    post {
        always {
            emailext(
                to: 'yousefsmn@gmail.com',
                subject: "${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Commit: ${GIT_COMMIT}, made by ${GIT_AUTHOR_NAME}, with message: ${GIT_COMMIT_MESSAGE}"
            )
        }
    }
}
