pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'web'
        CONTAINER_NAME = 'angry_moser'
        PORT_MAPPING = '8089:80'  // Adjust the port mapping as needed
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm 
            }
        }
            // stage('Checkout') {
            //     steps {
            //         deleteDir()
            //         checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/andrinahaura/project1.git']]])
            //     }
            // }
        
        stage('build docker') {
            steps {
                script {
                    // Run Docker container based on the built image
                   sh 'docker build -t web -f Dockerfile .'
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
