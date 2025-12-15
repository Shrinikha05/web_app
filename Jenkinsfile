pipeline {
    agent any

    environment {
        IMAGE_NAME = "shrinikha05/web_app"
        DOCKER_CREDENTIALS = "shrinikha05"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build(IMAGE_NAME)
                }
            }
        }

        stage('Test Docker Image') {
            steps {
                script {
                    sh "docker run --rm ${IMAGE_NAME} echo 'Container OK'"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
                        dockerImage.push('latest')
                    }
                }
            }
        }

    }

    post {
        always {
            sh "docker image prune -f"
        }
        success {
            echo "Pipeline finished successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
