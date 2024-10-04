pipeline {
    agent any

    tools {
        nodejs 'NodeJS 22.9.0' // This should match the name you gave in Global Tool Configuration
    }

    environment {
        DOCKER_IMAGE = 'ayo-pistis-webapp-img:latest' // Define your Docker image name
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull the source code from your Git repository
                git branch: 'main', url: 'https://github.com/Ayomidev/jenkins-repo.git'
            }
        }

        stage('Install Docker') {
            steps {
                script {
                    // Check if Docker is installed
                    def dockerCheck = sh(script: 'command -v docker || echo "Docker not found"', returnStdout: true).trim()

                    if (dockerCheck == "Docker not found") {
                        // If Docker is not found, install Docker using apt-get (for Ubuntu/Debian)
                        echo 'Docker not found. Installing docker.io...'
                        sh '''
                            sudo apt-get update
                            sudo apt-get install -y docker.io
                            sudo systemctl start docker
                            sudo systemctl enable docker
                        '''
                    } else {
                        echo "Docker is already installed: ${dockerCheck}"
                        sh 'docker --version' // Check Docker version
                    }
                }
            }
        }


        stage('Build') {
            steps {
                // Install dependencies (assuming a Node.js project)
                sh 'npm --version' // Verify npm is installed
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
