pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                export JAVA_HOME=/opt/java/jdk-25.0.3
                export PATH=$JAVA_HOME/bin:$PATH

                echo "JAVA_HOME=$JAVA_HOME"

                java -version
                javac -version

                chmod +x mvnw

                ./mvnw clean package -DskipTests
                '''
            }
        }
    }

    post {
        success {
            emailext(
                subject: "SpringBoot-PengSeyha SUCCESS",
                body: "SUCCESS BUILD\nBuild Number: ${BUILD_NUMBER}\nBuild URL: ${BUILD_URL}",
                to: "pengseyha2005@gmail.com"
            )
        }

        failure {
            emailext(
                subject: "SpringBoot-PengSeyha FAILED",
                body: "FAILED BUILD\nBuild Number: ${BUILD_NUMBER}\nBuild URL: ${BUILD_URL}\nConsole: ${BUILD_URL}console",
                to: "pengseyha2005@gmail.com"
            )
        }
    }
}