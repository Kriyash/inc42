pipeline {
    agent any
    
    triggers {
        githubPush()
    }
    
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('hello-world:latest')
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://hub.docker.com/repository/docker/yash1133/inc42/general', 'dockerhub_credentials') {
                        docker.image('hello-world:latest').push('latest')
                    }
                }
            }
        }
        stage('Deploy to Localhost') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub_credentials') {
                        docker.image('hello-world:latest').run('-p 9090:8080 --name hello-world-container')
                    }
                }
            }
        }
    }
    
    environment {
        DOCKER_HUB_USERNAME = credentials('yash1133')
        DOCKER_HUB_PASSWORD = credentials('Docker@123')
    }
}