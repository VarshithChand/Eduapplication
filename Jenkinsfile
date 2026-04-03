pipeline {
    agent any

    environment {
        IMAGE_NAME = "eduvault-app"
        DOCKER_USER = "varshithchand"   // your docker username
        IMAGE_TAG = "${DOCKER_USER}/${IMAGE_NAME}:latest"
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

        stage('Tag Image') {
            steps {
                sh 'docker tag $IMAGE_NAME $IMAGE_TAG'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-credentials',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push Image to Docker Hub') {
            steps {
                sh 'docker push $IMAGE_TAG'
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
                docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_TAG
                '''
            }
        }

    }

    post {
        success {
            echo "Docker Image Pushed & Container Running Successfully!"
        }
        failure {
            echo "Pipeline Failed!"
        }
    }
}
