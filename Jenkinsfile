pipeline {
    agent any

    environment {
        PROJECT_NAME = "SpringBoot_PengSeyha"
    }

    stages {
        stage('Check Java 25') {
            steps {
                sh '''
                ls -la /opt/java/jdk-25.0.3/bin/java
                /opt/java/jdk-25.0.3/bin/java -version
                '''
            }
        }

        stage('Build') {
            steps {
                withEnv([
                    'JAVA_HOME=/opt/java/jdk-25.0.3',
                    'PATH+JAVA=/opt/java/jdk-25.0.3/bin'
                ]) {
                    sh '''
                    echo "JAVA_HOME=$JAVA_HOME"
                    which java
                    java -version
                    ./mvnw clean package
                    '''
                }
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