pipeline {
    agent any

    environment {
        COMPOSE_FILE = 'docker-compose.yml'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/adhkar7/prometheus-project.git'
            }
        }

        stage('Build & Deploy') {
            steps {
                script {
                    echo "Stopping existing containers..."
                    sh 'docker compose down || true'

                    echo "Starting Prometheus + Grafana stack..."
                    sh 'docker compose up -d'
                }
            }
        }

        stage('Verify Containers') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        success {
            echo '✅ Monitoring stack deployed successfully!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
