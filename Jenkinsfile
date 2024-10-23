pipeline {
    agent any

    environment {
        GITHUB_REPO = 'https://github.com/rizkiramadhanx/vite-jenkins.git'
        DOCKER_COMPOSE_FILE = 'docker-compose.yml'
        IMAGE_NAME = 'vite-github'
    }

    stages {
        stage('Clone and Checkout Repository') {
            steps {
                git credentialsId: 'c3118073-2d40-41a6-ae76-62e2eee9f556', branch: 'development', url: "${GITHUB_REPO}"
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    // Build images using Docker Compose (on Windows)
                    bat "docker-compose -f ${DOCKER_COMPOSE_FILE} build"
                }
            }
        }

        stage('Update Services') {
            steps {
                script {
                    // Update services with new images (on Windows)
                    bat "docker-compose -f ${DOCKER_COMPOSE_FILE} up -d"
                }
            }
        }

        stage('Cleanup') {
            steps {
                script {
                    // Remove unused images (on Windows)
                    bat "docker image prune -f"
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline execution failed.'
        }
    }
}
