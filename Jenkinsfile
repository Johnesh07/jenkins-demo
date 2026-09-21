pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Building Docker application...'
                sh 'docker build -t aws-ec2-web-app .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Docker image...'
                sh 'docker image inspect aws-ec2-web-app'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'

                sh '''
                sudo docker stop aws-ec2-web-container 2>/dev/null || true
                sudo docker rm aws-ec2-web-container 2>/dev/null || true

                sudo docker run -d \
                  --name aws-ec2-web-container \
                  -p 8082:80 \
                  aws-ec2-web-app
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed.'
        }
    }
}
