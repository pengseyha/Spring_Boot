pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                export JAVA_HOME=/opt/java/jdk-25.0.3
                export PATH=$JAVA_HOME/bin:$PATH
                chmod +x mvnw
                ./mvnw clean package -DskipTests
                '''
            }
        }

        stage('Deploy with Ansible') {
            steps {
                sh '''
                ansible-playbook -i inventory.ini playbook.yml
                '''
            }
        }
    }

    post {
        success {
            emailext(
                subject: "SpringBoot-PengSeyha SUCCESS",
                body: "Build and deployment successful.\nURL: http://178.128.93.188/Midterm-2026/pengseyha\nBuild Number: ${BUILD_NUMBER}\nBuild URL: ${BUILD_URL}",
                to: "pengseyha2005@gmail.com"
            )
        }

        failure {
            emailext(
                subject: "SpringBoot-PengSeyha FAILED",
                body: "Build or deployment failed.\nBuild Number: ${BUILD_NUMBER}\nBuild URL: ${BUILD_URL}\nConsole: ${BUILD_URL}console",
                to: "pengseyha2005@gmail.com"
            )
        }
    }
}