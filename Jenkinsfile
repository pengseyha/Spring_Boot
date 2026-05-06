'pipeline {
    agent any

    // 1. Defining the environment globally is safer
    environment {
        JAVA_HOME = '/opt/java/jdk-25.0.3'
        // Prepend JDK 25 to the PATH so it is found first
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // 2. Use a single 'sh' block for environment and build
                sh '''
                    echo "Checking Java Version..."
                    java -version
                    
                    echo "Starting Build..."
                    chmod +x mvnw
                    ./mvnw clean package -DskipTests
                '''
            }
        }
    }

    post {
        failure {
            echo "Build failed. Check Java paths and permissions."
        }
    }
}'