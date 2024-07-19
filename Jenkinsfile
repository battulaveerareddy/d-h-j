pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = "battulaveerareddy/myimg"
        TAG = "v1"
        CONTAINER_NAME = "myimg-container"
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
                    docker build -t battulaveerareddy/myimg
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    docker run -d --name myimg-container -p 80:80 battulaveerareddy/myimg 
                }
            }
        }
    }
}
