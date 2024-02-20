pipeline {
    agent any
    
    environment {
        AWS_DEFAULT_REGION = 'us-east-1'  // Set your AWS region
        AMPLIFY_APP_ID = 'd90tsht2x16ht'  // Set your Amplify app ID
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm  // Checkout code from GitHub
            }
        }
        
        stage('Build') {
            steps {
                sh 'npm install'  // Install dependencies if any
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    sh 'zip -r myapp.zip .'  // Create a zip file of the code
                    sh "aws amplify start-job --app-id $AMPLIFY_APP_ID --branch-name master --file myapp.zip"  // Deploy the zip file
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
