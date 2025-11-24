pipeline {
    agent any

    environment {
        // Change path to your Tomcat webapps folder
        TOMCAT_WEBAPPS = "C:\\apache-tomcat-9.0.108\\webapps"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/nithish31105/selab5'
            }
        }

        stage('Clean') {
            steps {
                bat "mvn clean"
            }
        }

        stage('Install Dependencies') {
            steps {
                bat "mvn install"
            }
        }

        stage('Test') {
            steps {
                bat "mvn test"
            }
        }

        stage('Package WAR') {
            steps {
                bat "mvn package"
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                echo "Deploying WAR to Tomcat..."

                // Copy WAR to Tomcat webapps folder
                bat """
                copy target\\*.war "${env.TOMCAT_WEBAPPS}"
                """
            }
        }

        stage('Build Info') {
            steps {
                echo "Build Number: ${env.BUILD_NUMBER}"
            }
        }
    }

    post {

        success {
            emailext (
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hello,

Your Jenkins build was SUCCESSFUL.

Job: ${env.JOB_NAME}
Build: ${env.BUILD_NUMBER}

Application deployed to Tomcat.

Jenkins Server,
""",
                to: "your-email@gmail.com"
            )
        }

        failure {
            emailext (
                subject: "FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
Hello,

Your Jenkins build FAILED.

Job: ${env.JOB_NAME}
Build: ${env.BUILD_NUMBER}

Please check console output for errors.

Jenkins Server,
""",
                to: "your-email@gmail.com"
            )
        }
    }
}
