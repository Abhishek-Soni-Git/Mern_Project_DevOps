pipeline {
    agent any

    environment {
        DOCKERHUB_REPO_BACKEND = "abhi550/mean-backend"
        DOCKERHUB_REPO_FRONTEND = "abhi550/mean-frontend"
    }

    stages {

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t abhi550/mean-backend:latest backend'
            }
        }

        stage('Build Frontend Image') {
            steps {
                sh 'docker build -t abhi550/mean-frontend:latest frontend'
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh '''
                    echo $PASS | docker login -u $USER --password-stdin
                    docker push abhi550/mean-backend:latest
                    docker push abhi550/mean-frontend:latest
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker compose -f /home/ubuntu/mean-app/docker-compose.yml pull
                docker compose -f /home/ubuntu/mean-app/docker-compose.yml up -d
                '''
            }
        }
    }
}