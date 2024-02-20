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
        stage('Create Zip') {
            steps {
                script {
                    // Create a zip file from the built artifacts
                    sh 'zip -r myapp.zip build/*'
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Deploy the zip file to Amplify
                    sh 'aws amplify create-deployment --app-id d90tsht2x16ht --branch-name master --file myapp.zip''
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
