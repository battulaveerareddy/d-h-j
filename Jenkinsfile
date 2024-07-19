pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'battulaveerareddy/image:v1'
        DOCKERFILE_PATH = 'Dockerfile'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/battulaveerareddy/d-h-j.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}", "-f ${DOCKERFILE_PATH} .")
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    def dockerImage = docker.image("${DOCKER_IMAGE}")
                    dockerImage.inside('-p 8084:80') {
                        bat'echo "Container is running"'
                    }
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
