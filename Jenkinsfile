pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nest-js-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "shivampatil8101@gmail.com"
        PORT = "3000"
    }

    stages {
        stage('Clone Repo'){
            steps {
                git branch: 'main', url: 'https://github.com/shivam-patil-8101/CICD-jenkins.git'
            }
        }

        stage('Build Docker Image'){
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop & remove previuso container'){
            steps {
                sh '''
                    docker stop $CONTAINER_NAME || true
                    docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Docker Container Run'){
            steps {
                sh '''
                    docker run -d -p ${PORT}:${PORT} 
                    --name ${CONTAINER_NAME} ${IMAGE_NAME}
                '''
            }
        }

        stage('Send Email Notification'){
            steps {
                emailext(
                    subject: "NestJs App Deployed Succesfull",
                    body: "Your nest js app is deployed! http://16.171.208.17:${PORT}/",
                    to: "${EMAIL}"
                )
            }
        }
    }
}
