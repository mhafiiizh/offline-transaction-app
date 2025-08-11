pipeline {
    agent any

    environment {
        ENV_FILE = credentials('offline-transaction-app-env')
    }

    stages {
        stage('Prepare') {
            steps {
                echo "Menggunakan .env dari Jenkins credentials"
                sh """
                    cp "$ENV_FILE" .env
                """
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                sh """
                    docker compose down
                    docker compose up -d --build
                """
            }
        }
    }

    post {
        success {
            echo '✅ Deploy sukses!'
        }
        failure {
            echo '❌ Deploy gagal!'
        }
    }
}
