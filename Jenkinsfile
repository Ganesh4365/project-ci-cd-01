pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                script {
                    echo '🔄 Cloning repository...'
                    git branch: 'main', url: 'https://github.com/Ganesh4365/project-ci-cd-01.git'
                    echo '✅ Repository cloned successfully.'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo '⚙️ Building Docker image...'
                    docker.build('frontend-image')
                    echo '✅ Docker image built successfully.'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    echo '🚀 Running Docker container...'
                    // Remove existing container if it's already running
                    sh 'docker rm -f frontend-container || true'

                    // Run new container on port 80
                    sh 'docker run -d -p 80:80 --name frontend-container frontend-image'

                    echo '✅ Container is up and running on port 80.'
                }
            }
        }
    }
}
