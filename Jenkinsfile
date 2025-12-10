pipeline {
    agent any
    stages {
        stage('Email Test') {
            steps {
                emailext(
                    to: 'yousefsmn@gmail.com',
                    subject: "Test Email",
                    body: "This is a test email from Jenkins.",
                    mimeType: 'text/html'
                )
            }
        }
    }
}
