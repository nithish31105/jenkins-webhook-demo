pipeline {
    agent any

    environment {
        TOMCAT_WEBAPPS = "C:\\apache-tomcat-9.0.108\\webapps"
    }

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/nithish31105/selab5', branch: 'main'
            }
        }

        stage('Build & Test') {
            steps {
                bat "mvn clean install"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying WAR to Tomcat..."
                bat "copy target\\*.war \"${TOMCAT_WEBAPPS}\""
            }
        }
    }

    post {
        success {
            emailext(
                subject: "SUCCESS: ${JOB_NAME} #${BUILD_NUMBER}",
                body: "Build SUCCESS.\nJob: ${JOB_NAME}\nBuild: ${BUILD_NUMBER}\nWAR deployed to Tomcat.",
                to: "nithishthallada8217@gmail.com"
            )
        }

        failure {
            emailext(
                subject: "FAILED: ${JOB_NAME} #${BUILD_NUMBER}",
                body: "Build FAILED.\nJob: ${JOB_NAME}\nBuild: ${BUILD_NUMBER}\nCheck Jenkins console output.",
                to: "nithishthallada8217@gmail.com"
            )
        }
    }
}
