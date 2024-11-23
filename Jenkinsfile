pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                cleanWs()  // Clean workspace
                git url: 'https://github.com/AbdallahHesham44/public-repo.git', branch: 'main'
            }
        }
        stage('Run file') {
            steps {
                script {
                    sh 'chmod +x app1.sh'
                    sh './app1.sh'
                }
            }
        }
    }
}
