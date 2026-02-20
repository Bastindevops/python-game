pipeline {
    agent any

    environment {
        REPO_URL = "https://github.com/Bastindevops/python-game.git"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git credentialsId: 'BK',
                    url: "${REPO_URL}",
                    branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3001:3001 myapp:latest'
            }
        }
    }
}
