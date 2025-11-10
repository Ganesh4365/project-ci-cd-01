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
                echo 'Repository cloned successfully.'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker image...'
                    // Use current directory (.) as Docker build context
                    def app = docker.build("${IMAGE_NAME}", ".")
                    echo 'Docker image built successfully.'
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    echo 'Running Docker container...'

                    // Stop and remove old container if exists
                    sh """
                    docker ps -a | grep ${CONTAINER_NAME} && docker rm -f ${CONTAINER_NAME} || true
                    """

                    // Run the new container
                    sh """
                    docker run -d -p 80:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}
                    """

                    echo 'Container is up and running on port 80.'
                }
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed. Please check logs for details.'
        }
        success {
            echo 'Pipeline executed successfully!'
        }
    }
}
