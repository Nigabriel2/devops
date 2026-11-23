
pipeline {

    // Run the pipeline on an available Jenkins agent
    agent any

    // Define deployment variables
    environment {
        IMAGE_NAME = 'devops-app:2.0'
        CONTAINER_NAME = 'devops-container'
        HOST_PORT = '8081'
    }

    stages {

        // Stage 1: Retrieve source code from GitHub
        stage('Checkout') {
            steps {
                echo 'Retrieving project from GitHub...'
                checkout scm
            }
        }

        // Stage 2: Build the Docker image
        stage('Build') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        // Stage 3: Check the HTML file
        stage('Test') {
            steps {
                echo 'Checking index.html...'
                bat 'findstr /C:"Hello World from Jenkins!" index.html'
            }
        }

        // Stage 4: Deploy the application
        stage('Deploy') {
            steps {
                echo 'Deploying application to the target host...'

                // Remove the previous container if it exists
                bat 'docker rm -f %CONTAINER_NAME% 2>NUL || exit /b 0'

                // Run the new container
                bat 'docker run -d -p %HOST_PORT%:80 --name %CONTAINER_NAME% %IMAGE_NAME%'

                echo 'Deployment completed!'
            }
        }

    }

    post {
        success {
            echo 'Deployment successful!'
            echo 'Open http://localhost:8081 to view the application.'
        }

        failure {
            echo 'Deployment failed. Check the Jenkins Console Output.'
        }

        always {
            echo 'Jenkins pipeline execution completed.'
        }
    }
}
