pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t aws-ec2-web-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker rm -f aws-ec2-web-container 2>/dev/null || true'
                sh 'docker run -d --name aws-ec2-web-container -p 8082:80 aws-ec2-web-app'
            }
        }

        stage('Verify') {
            steps {
                sh 'docker ps'
                sh 'curl http://localhost:8082'
            }
        }
    }
}
