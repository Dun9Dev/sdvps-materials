pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/Dun9Dev/sdvps-materials.git', branch: 'main'
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
                    withCredentials([usernamePassword(
                        credentialsId: 'admin', 
                        usernameVariable: 'NEXUS_USER',
                        passwordVariable: 'NEXUS_PASSWORD'
                    )]) {
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
