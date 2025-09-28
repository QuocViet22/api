pipeline {
    agent any

    environment {
        APP_NAME = "api-app"
        JAR_NAME = "api-0.0.1-SNAPSHOT.jar"
        DEPLOY_DIR = "$WORKSPACE/deploy"
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
                sh '''
                    mkdir -p $DEPLOY_DIR
                    cd $DEPLOY_DIR

                    # Kill old process if running
                    if [ -f app.pid ]; then
                        kill -9 $(cat app.pid) || true
                        rm -f app.pid
                    fi

                    # Copy jar
                    cp $WORKSPACE/target/$JAR_NAME .

                    # Start new process
                    nohup java -jar $JAR_NAME --server.port=8080 > app.log 2>&1 &
                    echo $! > app.pid
                '''
            }
        }
    }
}
