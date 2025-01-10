pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "inessbk/myapp-backend:latest"  // Replace with your Docker image
        DOCKER_CREDENTIALS_ID = "docker-hub-credentials" // Replace with your Jenkins Docker credentials ID
    }
    stages {
        stage('Checkout Code') {
            steps {
                echo "Checking out source code..."
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                echo "Building Docker Image..."
                sh '''
                docker build -t $DOCKER_IMAGE .
                '''
            }
        }
        stage('Scan with Trivy') {
            steps {
                echo "Scanning Docker Image with Trivy..."
                sh '''
                trivy image $DOCKER_IMAGE || exit 1
                '''
            }
        }
        stage('Push Docker Image') {
            steps {
                echo "Pushing Docker Image to Docker Hub..."
                withCredentials([usernamePassword(credentialsId: "$DOCKER_CREDENTIALS_ID", usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh '''
                    echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                    docker push $DOCKER_IMAGE
                    '''
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                echo "Deploying to Kubernetes..."
                sh '''
                kubectl apply -f kubernetes/deployment.yaml
                '''
            }
        }
    }
    post {
        always {
            echo "Cleaning up..."
            sh 'docker system prune -f'
        }
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed."
        }
    }
}
