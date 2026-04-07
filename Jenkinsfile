pipeline {
    agent any

    environment {
        APP_DIR = "docker-fastapi-test"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/RohitPatil18/docker-fastapi-test'
            }
        }

        stage('Build & Deploy') {
            steps {
                dir("${APP_DIR}") {
                    sh 'docker-compose down'
                    sh 'docker-compose up -d --build'
                }
            }
        }

        stage('Health Check') {
            steps {
                sh 'sleep 5'
                sh 'curl -f http://localhost:8000/ || exit 1'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
