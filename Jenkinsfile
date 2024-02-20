pipeline {
    agent any
    
    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        AMPLIFY_APP_ID = 'd90tsht2x16ht'
        S3_BUCKET_NAME = 'php-bucket11'
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
                sh 'zip -r myapp.zip build/'
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    // Upload the zip file to S3
                    sh "aws s3 cp myapp.zip s3://${S3_BUCKET_NAME}/"
                    
                    // Start deployment from S3
                    def deployCommand = "aws amplify start-deployment --app-id ${AMPLIFY_APP_ID} --branch-name master --source-url s3://${S3_BUCKET_NAME}/myapp.zip"
                    sh deployCommand
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
