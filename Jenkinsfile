pipeline {
    agent any
    environment {
        // Set these globally for the whole pipeline
        JAVA_HOME = '/opt/java/jdk-25.0.3'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                    # This will now correctly show JDK 25
                    java -version
                    
                    # Ensure mvnw is executable
                    chmod +x mvnw
                    
                    # Run the build
                    ./mvnw clean package
                '''
            }
        }
    }
}