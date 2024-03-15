pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Checkout the source code from the Git repository
                checkout scm
                
                // Build the Docker image
                script {
                    docker.build('hello-world:latest')
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                // Push the Docker image to Docker Hub
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials') {
                        docker.image('hello-world:latest').push('latest')
                    }
                }
            }
        }
        stage('Deploy to Localhost') {
            steps {
                // Deploy the Docker container to localhost:9090
                script {
                    docker.withRegistry('', 'dockerhub_credentials') {
                        docker.image('hello-world:latest').run('-p 9090:8080 --name hello-world-container')
                    }
                }
            }
        }
    }
    
    // Define the credentials for Docker Hub
    environment {
        dockerhub_credentials = 'dockerhub_credentials'
    }
}
