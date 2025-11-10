pipeline {
    agent any

    environment {
        IMAGE_NAME = "frontend-image"
        CONTAINER_NAME = "frontend-container"
    }

    stages {
        stage('Clean Workspace') {
            steps {
                cleanWs()
                echo 'Workspace cleaned.'
            }
        }

        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/Ganesh4365/project-ci-cd-01.git'
            }
        }

        stage('Verify Docker Access') {
            steps {
                sh 'whoami'
                sh 'docker --version'
                sh 'docker ps'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker image...'
                    sh 'docker build -t frontend-image .'
                    echo 'Docker image built successfully.'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    echo 'Running Docker container...'
                    // Stop and remove old container if exists
                    sh 'docker rm -f frontend-container || true'

                    // Run the new container
                    sh 'docker run -d -p 80:80 --name frontend-container frontend-image'

                    echo 'Container is up and running on port 80.'
                }
            }
        }

        stage('Check Running Container') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline completed successfully.'
        }
        failure {
            echo '❌ Pipeline failed. Check logs above.'
        }
    }
}
