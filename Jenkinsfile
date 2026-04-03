pipeline {
    agent any

    environment {
        IMAGE_NAME = "eduvault-app"
        DOCKER_USER = "varshithchand"
        IMAGE_TAG = "${DOCKER_USER}/${IMAGE_NAME}:latest"
        CONTAINER_NAME = "eduvault-container"
        PORT = "5000"
    }

    stages {

        stage('Cleanup Docker Space') {
            steps {
                sh '''
                echo "Cleaning unused Docker data..."
                docker system prune -a -f || true
                docker volume prune -f || true
                docker builder prune -a -f || true
                '''
            }
        }

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

        stage('Tag Docker Image') {
            steps {
                sh 'docker tag $IMAGE_NAME $IMAGE_TAG'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-credentials',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
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
                docker run -d -p $PORT:$PORT --name $CONTAINER_NAME $IMAGE_TAG
                '''
            }
        }

    }

    post {
        success {
            echo "✅ Build, Push & Deployment Successful!"
        }
        failure {
            echo "❌ Pipeline Failed! Check logs."
        }
    }
}
