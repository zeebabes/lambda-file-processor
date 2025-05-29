pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key-id')     // from Jenkins credentials
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key') // from Jenkins credentials
        AWS_REGION = 'us-east-2'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/zeebabes/lambda-file-processor.git', branch: 'test-build'
            }
        }

        stage('Zip Lambda Function') {
            steps {
                bat 'powershell Compress-Archive -Path lambda_function.py -DestinationPath lambda_function_payload.zip -Force'

            }
        }

        stage('Terraform Init') {
            steps {
                bat 'terraform init'
            }
        }

        stage('Terraform Apply') {
            steps {
                bat 'terraform apply -auto-approve'
            }
        }
    }
}
