pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_CREDENTIALS_ID = 'battulaveerareddy'
    }

    stages {
        stage('Checkout') {
            steps {
                git url:'https://github.com/battulaveerareddy/d-h-j.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def tagName = "v1"
                    def imageName = "battulaveerareddy/image:${tagName}"
                    
                    docker.build(imageName, "-f Dockerfile .")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    def tagName = "v1"
                    def imageName = "battulaveerareddy/image:${tagName}"
                    docker.withRegistry("https://index.docker.io/v1/", DOCKER_CREDENTIALS_ID) {
                        docker.image(imageName).push()
                    }
                }
            }
        }


        stage('Run Docker Container') {
            steps {
                script {
                    def tagName = "v1"
                    def containerName = "container-${tagName}"
                    def imageName = "battulaveerareddy/image:${tagName}"
                     bat "docker rm -f ${containerName} || true"
                    bat "docker run -d -p 8051:80 --name ${container} ${battulaveerareddy/image}"
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
