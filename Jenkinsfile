pipeline {
    agent any

    environment {
        REPO_URL = "https://github.com/Bastindevops/python-game.git"
        IMAGE_NAME = "YOUR_DOCKERHUB_USERNAME/myapp:latest"
        DOCKER_CREDS = credentials('dockerhub')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    credentialsId: 'BK',
                    url: "${REPO_URL}"
            }
        }

        stage('Docker Login') {
            steps {
                bat '''
                echo $DOCKER_CREDS_PSW | docker login -u $DOCKER_CREDS_USR --password-stdin
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                bat "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                docker rm -f myapp || true
                docker run -d --name myapp -p 3001:3001 ${IMAGE_NAME}
                '''
            }
        }

        stage('Push Image') {
            steps {
                bat "docker push ${IMAGE_NAME}"
            }
        }
    }

    post {
        always {
            bat 'docker logout'
        }
    }
}
