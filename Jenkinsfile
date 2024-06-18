pipeline {
    agent any

    environment {
        CONTAINER_NAME = "my-app"
        DATABASE_NAME = "MyDatabase"
        DATABASE_PASSWORD = "dutran3802"
        DATABASE_ROOT_PASSWORD = "dutran3802"
        DATABASE_USER = "admin"
    }

    stages {
        stage('Checkout') {
            steps {
                // Lấy mã nguồn từ repository
                git credentialsId: 'my-git', url: 'https://github.com/Du380202/wordpress.git', branch: 'main'
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Xây dựng và triển khai bằng Docker Compose
                    bat 'docker-compose down'



                    // Chỉ khởi động lại dịch vụ WordPress
                    bat 'docker-compose up --build'
                }
            }
        }

        stage('Post-deploy Cleanup') {
            steps {
                // Bất kỳ bước dọn dẹp nào sau triển khai, nếu cần
                bat 'docker system prune -f'
            }
        }
    }

    post {
        always {
            // Luôn luôn lưu trữ log
            archiveArtifacts artifacts: '**/logs/**', allowEmptyArchive: true
        }
    }
}
