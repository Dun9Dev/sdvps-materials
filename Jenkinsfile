pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Dun9Dev/sdvps-materials.git', branch: 'main'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'go test .'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build .'
            }
        }
    }
}
