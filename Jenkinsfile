pipeline {
    agent any
    
    environment {
        DOCKER_IMAGE = 'my-image'
        CONTAINER_NAME = 'my-container'
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
                    docker.build("${my-image}:${env.BUILD_NUMBER}", "-f Dockerfile .")
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    docker.run("${my-image}:${env.BUILD_NUMBER}", "--name ${my-container} -d -p 80:80")
                }
            }
        }
    }
}
