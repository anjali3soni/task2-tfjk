pipeline {
    agent any

    tools {
        nodejs 'NodeJS' 
    }
    
    environment {
        AWS_REGION = 'us-east-2'
        S3_BUCKET = 'react-app-bucket-abc' 
        PATH = "/usr/local/bin:$PATH"
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/anjali3soni/task2-tfjk.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Deploy to S3') {
            steps {
                sh '''
                aws s3 sync build/ s3://$S3_BUCKET/ --region $AWS_REGION
                '''
            }
        }
    }
}
