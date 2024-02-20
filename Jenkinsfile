pipeline {
    agent any
    environment {
        AWS_DEFAULT_REGION = 'us-east-1' // Set your AWS region
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Add steps to build your project, if necessary'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    // Assuming you have configured AWS CLI and your Amplify app is connected to the GitHub repo
                    // Replace 'yourAmplifyAppId' with your actual Amplify app ID and 'yourBranchName' with the branch you want to deploy
                    sh 'aws amplify start-job --app-id d3g3ff7letaeke --branch-name master --job-type RELEASE'
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
