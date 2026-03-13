pipeline {
    agent any

    environment {
        IMAGE_NAME = "eduvault-app"
        CONTAINER_NAME = "eduvault-container"
        PORT = "5000"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/VarshithChand/Eduapplication.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Existing Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME
                '''
            }
        }

    }

    post {
        success {
            echo "Docker Image Built and Container Running Successfully!"
        }
        failure {
            echo "Pipeline Failed!"
        }
    }
}
