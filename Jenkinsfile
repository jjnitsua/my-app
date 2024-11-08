pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_VERSION = '1.29.2' // Set your Docker Compose version
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/jjnitsua/my-app.git'
            }
        }

        stage('Build and Deploy') {
            steps {
                script {
                    // Pull the latest images and start containers
                    sh 'docker-compose down' // Clean up old containers if any
                    sh 'docker-compose pull'
                    sh 'docker-compose up -d --build'
                }
            }
        }

        stage('Health Check') {
            steps {
                script {
                    // Test if the app is running by hitting the health endpoint
                    sh 'curl -f http://localhost:3000 || exit 1'
                }
            }
        }
    }

    post {
        always {
            // Clean up
            sh 'docker-compose down'
        }
    }
}
