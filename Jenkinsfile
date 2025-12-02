pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: "https://github.com/nithish31105/jenkins-webhook.git"
            }
        }

        stage('Build') {
            steps {
                echo "Building the project…"
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
            }
        }
    }

    post {
        success {
            emailext(
                to: "youremail@gmail.com",
                subject: "BUILD SUCCESS - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build succeeded."
            )
        }
        failure {
            emailext(
                to: "youremail@gmail.com",
                subject: "BUILD FAILED - ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build failed. Please check Jenkins console output."
            )
        }
    }
}
