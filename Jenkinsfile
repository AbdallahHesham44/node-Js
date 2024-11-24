pipeline {
    agent any
    
    environment {
        // Docker Hub configurations
        DOCKERHUB_CREDENTIALS = credentials('DOCKERHUB_CREDENTIALS')
        DOCKER_HUB_USERNAME = 'abdallah1312'
        IMAGE_NAME = 'my-node-app'
        IMAGE_TAG = "${BUILD_NUMBER}"

        EC2_HOST ='52.73.65.200'  // Just the IP address without ec2-user@
        EC2_USER = 'ec2-user'
        SSH_KEY  = credentials('ssh_cred')

    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AbdallahHesham44/node-Js.git'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    sh 'node app.js'
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_HUB_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG} ."
                    sh "docker tag ${DOCKER_HUB_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG} ${DOCKER_HUB_USERNAME}/${IMAGE_NAME}:latest"
                }
            }
        }
        
        stage('Login to Docker Hub') {
            steps {
                script {
                    sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                script {
                    sh "docker push ${DOCKER_HUB_USERNAME}/${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
       stage('Deploy to EC2') {
            steps {
                script {
                    // Copy the SSH key to a temporary location
                    withCredentials([sshUserPrivateKey(credentialsId: 'ssh_cred', keyFileVariable: 'SSH_KEY')]) {
                        sh '''
                            # SSH into EC2 and run Docker container
                            ssh -o StrictHostKeyChecking=no -i ${SSH_KEY} ${EC2_USER}@${EC2_HOST}  '
                                # Pull the latest image
                                docker pull abdallah1312/my-node-app:8
                                
                                # Stop and remove existing container if it exists
                                docker stop node-app-AbdallahHesham || true
                                docker rm node-app-AbdallahHesham || true
                                
                                # Run the new container
                                docker run -d \
                                    --name node-app-AbdallahHesham \
                                    -p 1312:3000 \
                                    abdallah1312/my-node-app:8
                            '
                        '''
                    }
                }
            }
        } 
    }
    
    post {
        always {
            sh 'docker logout'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
