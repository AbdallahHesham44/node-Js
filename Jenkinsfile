pipeline {
    agent any

    environment {
        // Define Docker Hub credentials
        DOCKER_HUB_CREDENTIALS = credentials('Docker_secret')
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
                    // Use the credentials securely to login and push the Docker image
                    withCredentials([usernamePassword(credentialsId: 'Docker_secret', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                        // Login to Docker Hub using credentials
                        sh 'echo $DOCKER_HUB_PASSWORD | docker login -u $DOCKER_HUB_USERNAME --password-stdin'
                        // Push the Docker image
                        docker.image("${IMAGE_NAME}:${IMAGE_TAG}").push()
                        // Logout from Docker Hub
                        sh 'docker logout'
                    }
                }
            }
        }
    }
}
