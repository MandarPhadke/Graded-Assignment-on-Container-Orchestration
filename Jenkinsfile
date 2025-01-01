pipeline {
    agent any
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('docker-hub')
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/UnpredictablePrashant/learnerReportCS_frontend'
                git 'https://github.com/UnpredictablePrashant/learnerReportCS_backend'
            }
        }
        stage('Build Docker Images') {
            steps {
                script {
                    sh 'docker build -t unpredictableprashant/learnerReportCS_frontend ./frontend'
                    sh 'docker build -t unpredictableprashant/learnerReportCS_backend ./backend'
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('', DOCKER_HUB_CREDENTIALS) {
                        sh 'docker push unpredictableprashant/learnerReportCS_frontend'
                        sh 'docker push unpredictableprashant/learnerReportCS_backend'
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh 'helm upgrade --install learner-report ./helm'
            }
        }
    }
}
