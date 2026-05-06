pipeline {
    agent any

    environment {
        PROJECT_NAME = "SpringBoot_PengSeyha"
        JAVA_HOME = "/opt/java/jdk-25.0.3"
        PATH = "/opt/java/jdk-25.0.3/bin:${env.PATH}"
    }

    stages {
        stage('Check Java Version') {
            steps {
                sh '''
                java -version
                echo $JAVA_HOME
                '''
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

Check console output:
${BUILD_URL}console
""",
                to: 'pengseyha2005@gmail.com',
                from: 'pengseyha2005@gmail.com'
            )
        }
    }
}