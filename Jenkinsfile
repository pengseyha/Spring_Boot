pipeline {
    agent any

    environment {
        PROJECT_NAME = "SpringBoot_PengSeyha"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/pengseyha/Spring_Boot.git'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean package'
            }
        }
    }

    post {

        success {
            emailext(
                subject: "SpringBoot_PengSeyha SUCCESS",
                body: """
SUCCESS BUILD

Project: ${PROJECT_NAME}
Build Number: ${BUILD_NUMBER}
Build URL: ${BUILD_URL}
""",
                to: 'pengseyha2005@gmail.com'
            )
        }

        failure {
            emailext(
                subject: "SpringBoot_PengSeyha FAILED",
                body: """
FAILED BUILD

Project: ${PROJECT_NAME}
Build Number: ${BUILD_NUMBER}
Build URL: ${BUILD_URL}

Check console output for stacktrace.
""",
                to: 'pengseyha2005@gmail.com'
            )
        }
    }
}
