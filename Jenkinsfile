pipeline {
    agent any

    environment {
        DOCKERHUB_REPO_BACKEND = "abhi550/mean-backend"
        DOCKERHUB_REPO_FRONTEND = "abhi550/mean-frontend"
        IMAGE_TAG = "latest"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend Image') {
            steps {
                sh """
                    docker build -t ${DOCKERHUB_REPO_BACKEND}:${IMAGE_TAG} backend
                """
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh """
                    docker build -t ${DOCKERHUB_REPO_FRONTEND}:${IMAGE_TAG} frontend
                """
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                        echo \$DOCKER_PASS | docker login -u \$DOCKER_USER --password-stdin
                        docker push ${DOCKERHUB_REPO_BACKEND}:${IMAGE_TAG}
                        docker push ${DOCKERHUB_REPO_FRONTEND}:${IMAGE_TAG}
                        docker logout
                    """
                }
            }
        }

        stage('Deploy') {
            steps {
                sh """
                    docker compose -f /home/ubuntu/mean-app/docker-compose.yml pull
                    docker compose -f /home/ubuntu/mean-app/docker-compose.yml up -d
                """
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline executed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Check logs above."
        }
    }
}