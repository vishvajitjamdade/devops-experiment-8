pipeline {
    agent any

    environment {
        registry = "world_winner/devops-experiment-8"
        registryCredential = "dockerhub-credentials"
        dockerImage = ""
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/vishvajitjamdade/devops-experiment-8.git'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${env.BUILD_ID}")
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'npm test'
                    }
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', registryCredential) {
                        dockerImage.push()
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
