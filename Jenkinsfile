pipeline {
    agent any

    tools {
        nodejs 'NodeJS' 
    }
    
    environment {
        AWS_REGION = 'ap-south-1'
        S3_BUCKET = 'react-app-bucket-abc' 
        PATH = "/usr/local/bin:$PATH"
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Dhruv-Bagora/react-app-jenkins.git'
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
