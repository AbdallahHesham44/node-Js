pipeline {
    agent any

    environment {
        
        // Define Docker Hub credentials
        DOCKERHUB_CREDENTIALS_USR = credentials('docker_acc')
        // Replace with your Docker Hub username
        DOCKER_HUB_USERNAME = 'abdallah1312'
        // Image name and tag to be used
        IMAGE_NAME = "${DOCKER_HUB_USERNAME}/my-node-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                cleanWs()  // Clean workspace
                git url: 'https://github.com/AbdallahHesham44/node-Js.git', branch: 'main'
            }
        }

        stage('Build and Test Node.js Application') {
            steps {
                script {
                    // Install dependencies
                    sh 'npm install'
                    // Test the Node.js app (optional)
                    sh 'node app.js'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                        sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin" {
                        // Push the Docker image
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
              
                    }
                }
            }
        }
    }
}
