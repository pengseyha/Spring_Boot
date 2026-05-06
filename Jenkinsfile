pipeline {
    agent any

    environment {
        PROJECT_NAME = "SpringBoot_PengSeyha"
    }

    stages {

        stage('Build') {
            steps {
                sh '''
                export JAVA_HOME=/opt/java/jdk-25.0.3
                export PATH=$JAVA_HOME/bin:$PATH

                echo "JAVA_HOME=$JAVA_HOME"
                which java
                java -version

                ./mvnw clean package
                '''
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

Check console output:
${BUILD_URL}console
""",
                to: 'pengseyha2005@gmail.com'
            )
        }
    }
}