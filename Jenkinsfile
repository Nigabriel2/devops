
pipeline {
    agent any

    environment {
        IMAGE_NAME = 'devops-app:2.0'
        CONTAINER_NAME = 'devops-container'
        HOST_PORT = '8084'
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Retrieving project from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t "$IMAGE_NAME" .'
            }
        }

        stage('Test') {
            steps {
                echo 'Checking index.html...'
                sh 'grep -Fq "Hello World from DevOps!" index.html'
                echo 'HTML test passed!'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                sh 'docker rm -f "$CONTAINER_NAME" || true'

                sh 'docker run -d -p "${HOST_PORT}:80" --name "$CONTAINER_NAME" "$IMAGE_NAME"'

                echo 'Deployment completed!'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
            echo 'Open http://localhost:8084 to view the application.'
        }

        failure {
            echo 'Deployment failed. Check Jenkins Console Output.'
        }

        always {
            echo 'Jenkins pipeline execution completed.'
        }
    }
}

