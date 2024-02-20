pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = 'us-east-1' 
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    // Install dependencies and build the project
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Create a deployment
                    sh 'aws amplify create-deployment --app-id YOUR_AMPLIFY_APP_ID --branch-name master '
                    // Start the deployment
                    sh 'aws amplify start-deployment --app-id d90tsht2x16ht --branch-name master'
                }
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
