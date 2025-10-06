pipeline {
    agent any

    environment {
        dockerImage = "world_winner/devops-experiment-8:7"
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/vishvajitjamdade/devops-experiment-8.git'
            }
        }

        stage('Build Image') {
            steps {
                bat "docker build -t ${dockerImage} ."
            }
        }

        stage('Test Image') {
    steps {
        bat """
        docker run --rm -v "%cd%:/app" -w /app ${dockerImage} sh -c "echo Hello from container && ls -la"
        """
    }
}


        stage('Push Image') {
            steps {
                // Push only if needed
                bat "docker push ${dockerImage}"
            }
        }
    }
}
