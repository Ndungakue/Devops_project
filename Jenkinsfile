pipeline {
    agent any
    
    environment {
        DOCKER_HUB_REPO = 'ndungakue/portfolio'
        DOCKER_HUB_CRED = 'dockerhub-credentials'
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_HUB_REPO}:${BUILD_NUMBER}")
                }
            }
        }
        
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_HUB_CRED) {
                        docker.image("${DOCKER_HUB_REPO}:${BUILD_NUMBER}").push()
                        docker.image("${DOCKER_HUB_REPO}:${BUILD_NUMBER}").push('latest')
                    }
                }
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
} 