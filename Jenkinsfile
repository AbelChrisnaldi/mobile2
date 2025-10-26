pipeline {
    agent any

    environment {
        IMAGENAME = 'abelchris/notes-app'
        REGISTRY = 'https://index.docker.io/v1/'
        REGISTRYCREDENTIALS = 'dockerhub-credentials'
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
                    dockerImage = docker.build("${IMAGENAME}:${env.BUILD_NUMBER}")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry("${REGISTRY}", "${REGISTRYCREDENTIALS}") {
                        dockerImage.push()
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}
