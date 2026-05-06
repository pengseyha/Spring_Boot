pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh '''
                export JAVA_HOME=/opt/java/jdk-25.0.3
                export PATH=$JAVA_HOME/bin:$PATH

                java -version
                javac -version

                chmod +x mvnw

                ./mvnw clean package -DskipTests
                '''
            }
        }

        stage('Deploy') {
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
                subject: "SpringBoot-PengSeyha Build Success",
                body: """
Build Success! Website:
http://178.128.93.188/Midterm-2026/pengseyha
""",
                to: "pengseyha2005@gmail.com"
            )
        }

        failure {
            emailext(
                subject: "SpringBoot-PengSeyha Build Failed",
                body: """
Build Failed!

Check Console Output:
${BUILD_URL}console
""",
                to: "pengseyha2005@gmail.com"
            )
        }
    }
}