pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('DOCKERHUB_CREDENTIALS')
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/AbdallahHesham44/node-Js.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'node app.js'
                }
            }
        }
        stage('Docker Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t abdallah1312/my-node-app:2 .'
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                sh 'docker push abdallah1312/my-node-app:2'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
