pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'ayo-pistis-webapp-img:latest' // Define your Docker image name
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull the source code from your Git repository
                git 'https://github.com/Ayomidev/jenkins-repo.git'
            }
        }

        stage('Build') {
            steps {
                // Install dependencies (assuming a Node.js project)
                sh 'npm install'
            }
        }

        stage('Test') {
            steps {
                // Run tests (assuming a Node.js project)
                sh 'npm test'
            }
        }

        stage('Package') {
            steps {
                // Build the Docker image using the Dockerfile and package.json
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the Docker image (e.g., push to a registry or run the container)
                script {
                    // Example: pushing to DockerHub or any other container registry
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-credential') {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
