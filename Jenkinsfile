pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'yourusername/your-static-site:latest'
        CONTAINER_NAME = 'your-container-name'
        PORT_MAPPING = '8081:80'  // Adjust the port mapping as needed
    }

    stages {
        stage('Checkout') {
            steps {
                // Clean workspace before checkout
                deleteDir()
                // Checkout the HTML source code from GitHub
                git url: 'https://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@github.com/andrinahaura/project1.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image with the HTML content
                    docker.build("${DOCKER_IMAGE}", '-f Dockerfile .')
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run Docker container based on the built image
                    docker.image("${DOCKER_IMAGE}").run("-p ${PORT_MAPPING} --name ${CONTAINER_NAME}")
                }
            }
        }
    }

    post {
        always {
            script {
                // Stop and remove the Docker container after execution
                docker.image("${DOCKER_IMAGE}").stop()
                docker.image("${DOCKER_IMAGE}").remove()
            }
        }
    }
}