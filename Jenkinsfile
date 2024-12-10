pipeline {
    agent any
    environment {
        DOCKER_REGISTRY = 'igwefredrickchiemeka@gmail.com'
    }
    stages {
        stage('Docker Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'docker-credentials-id', 
                                                     usernameVariable: 'DOCKER_USERNAME', 
                                                     passwordVariable: 'DOCKER_PASSWORD')]) {
                        sh """
                        echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin $DOCKER_REGISTRY
                        """
                    }
                }
            }
        }
        stage('Build & Push Image') {
            steps {
                script {
                    sh """
                    docker build -t ${DOCKER_REGISTRY}/weatherapp .
                    docker push ${DOCKER_REGISTRY}/weatherapp
                    """
                }
            }
        }
    }
    post {
        always {
            sh 'docker logout $DOCKER_REGISTRY'
        }
    }
}
