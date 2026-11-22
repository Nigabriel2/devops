
pipeline {

    // Run on any available Jenkins agent
    agent any

    // Define pipeline stages
    stages {

        // Stage 1: Build Docker image
        stage('Build') {
            steps {

                echo 'Starting DevOps application build...'

                // Check Docker availability
                sh 'docker --version'

                // Build Docker image
                sh 'docker build -t devops-app:1.0 .'

                echo 'Docker image build completed!'
            }
        }
    }

    // Actions after pipeline execution
    post {

        success {
            echo 'SUCCESS: DevOps application built successfully.'
        }

        failure {
            echo 'FAILURE: Check the Jenkins Console Output.'
        }

        always {
            echo 'Jenkins pipeline execution finished.'
        }
    }
}
