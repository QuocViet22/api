pipeline {
    agent any

    tools {
        maven 'Maven3'   // configure in Jenkins: Manage Jenkins -> Global Tool Configuration
        jdk 'JDK17'      // configure Java version
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/QuocViet22/api.git'
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean package -DskipTests"
            }
        }
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
