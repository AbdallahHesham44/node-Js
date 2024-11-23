pipeline {
    agent any
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
                   
                    sh 'node app1.sh'
                }
            }
        }
    }
}
