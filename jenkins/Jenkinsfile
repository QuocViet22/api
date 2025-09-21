pipeline {
    agent any

    tools {
        maven 'Maven3' // Make sure Maven3 is configured in Jenkins (Manage Jenkins > Global Tool Configuration)
        jdk 'Java17'   // Adjust JDK version to match your project
    }

    environment {
        JAR_NAME = "api-0.0.1-SNAPSHOT.jar"  // Name for built jar
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/QuocViet22/api.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                // Kill old process if running
                sh 'pkill -f "$JAR_NAME" || true'

                // Copy jar from target folder
                sh 'cp target/*.jar $JAR_NAME'

                // Run jar in background
                sh 'nohup java -jar $JAR_NAME --server.port=9090 > app.log 2>&1 &'
            }
        }
    }
}
