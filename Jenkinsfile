pipeline {
    agent any

    environment {
        PROJECT_NAME = "SpringBoot_PengSeyha"
    }

    stages {
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
                to: 'pengseyha2005@gmail.com',
                from: 'pengseyha2005@gmail.com'
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

Check console output for stacktrace:
${BUILD_URL}console
""",
                to: 'pengseyha2005@gmail.com',
                from: 'pengseyha2005@gmail.com'
            )
        }
    }
}