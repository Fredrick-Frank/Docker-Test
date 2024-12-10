pipeline {
    agent any
    environment {
        DOCKER_REGISTRY = 'igwefredrickchiemeka@gmail.com'
        DOCKER_USERNAME = 'igfred' // Set Docker username as plaintext or parameter
    }
    stages {
        stage('Docker Login') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'docker-credentials-id', variable: 'docker-credentials-id')]) {
                        sh """
                        echo "$docker-credentials-id" | docker login -u $DOCKER_USERNAME --password-stdin $DOCKER_REGISTRY
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
            sh 'docker logout $DOCKER_REGISTRY' // Always logout after pushing
        }
    }
}
