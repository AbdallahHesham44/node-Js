pipeline {
    agent any
     environment {
        // Define Docker Hub credentials
        DOCKER_HUB_CREDENTIALS = credentials('dockerhub-credentials-id')
        // Replace with your Docker Hub username
        DOCKER_HUB_USERNAME = 'abdallah1312'
        // Image name and tag to be used
        IMAGE_NAME = "${DOCKER_HUB_USERNAME}/my-node-app"
        IMAGE_TAG = 'v1.0'
    }

    stages {
        stage('Checkout') {
            steps {
                cleanWs()  // Clean workspace
                git url: 'https://github.com/AbdallahHesham44/node-Js.git', branch: 'main'
            }
        }
        stage('build') {
            steps {
                script {
                   
                    sh 'node app.js'
                }
            }
        }
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }
stages {
        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using credentials
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') {
                        // Push the Docker image
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
                    }
                }
            }
        }
    }
   post {
        always {
            // Clean up local Docker images after the build
            script {
                docker.image("${IMAGE_NAME}:${IMAGE_TAG}").remove()
            }
        }
    }
}
