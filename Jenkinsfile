pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_CREDENTIALS_ID = 'dockerHubCredentials'
        IMAGE_NAME = "battulaveerareddy/my-img"
        TAG = "v1"
        CONTAINER_NAME = "my-cntr"
    }
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/battulaveerareddy/d-h-j.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    def dockerImage = "${battulaveerareddy/my-img}:${v1}"
                    docker.build(dockerImage, "-f Dockerfile .")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    def dockerImage = "${battulaveerareddy/my-img}:${v1}"
                    docker.withRegistry(DOCKER_REGISTRY, DOCKER_CREDENTIALS_ID) {
                        docker.image(dockerImage).push()
                    }
                }
            }
        }
        
        stage('Deploy Docker Container') {
            steps {
                script {
                    bat "docker rm -f ${my-cntr} || true"
                    def dockerImage = "${battulaveerareddy/my-img}:${v1}"
                    bat"docker run -d -p 80:80 --name ${my-cntr} ${battulaveerareddy/my-img}"
                }
            }
        }
    }
}
