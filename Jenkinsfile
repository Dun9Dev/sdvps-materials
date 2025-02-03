pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/ваш-логин/название-репозитория.git', branch: 'main'
            }
        }
        stage('Build Go Binary') {
            steps {
                sh 'go build -o app main.go'
            }
        }
        stage('Upload to Nexus') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'nexus-credentials', usernameVariable: 'NEXUS_USER', passwordVariable: 'NEXUS_PASSWORD')]) {
                        sh """
                            curl -u \$NEXUS_USER:\$NEXUS_PASSWORD \
                            --upload-file app \
                            http://ваш-ip-адрес:8081/repository/имя-репозитория/app
                        """
                    }
                }
            }
        }
    }
}
