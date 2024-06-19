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
                git credentialsId: 'd162f298-f188-4150-9987-e5b92f62b5d4', url: 'https://github.com/Du380202/wordpress.git', branch: 'main'
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    bat 'docker-compose down'
                    bat 'docker-compose up --build'
                }
            }
        }

        stage('Post-deploy Cleanup') {
            steps {
                bat 'docker system prune -f'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/logs/**', allowEmptyArchive: true
        }
    }
}
