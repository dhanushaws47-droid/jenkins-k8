pipeline {
    agent any

    environment {
        IMAGE = "dhanushdock1/mysite:${BUILD_NUMBER}"
    }

    stages {

        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t $IMAGE .'
            }
        }

        stage('Docker Push') {
            steps {
                sh 'docker push $IMAGE'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl set image deployment/demo-deployment \
                demo-container=$IMAGE
                kubectl rollout status deployment/demo-deployment
                '''
            }
        }
    }
}
