pipeline {
    agent any

    environment {
        ENV_FILE = credentials('offline-transaction-app-env')
    }

    stages {
        stage('Prepare') {
            steps {
                echo "Menggunakan .env dari Jenkins credentials"
                bat """
                    copy "%ENV_FILE%" .env
                """
                echo "Database endpoint: ${env.DATABASE_ENDPOINT}"

            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                bat """
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
