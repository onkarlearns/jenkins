pipeline {
    agent any
    environment {
        REGISTRY = 'ghcr.io'
        IMAGE_NAME = 'onkarlearns/jenkins'
    }
    stages {
        stage('Install') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                    docker build -t ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} \
                               -t ${REGISTRY}/${IMAGE_NAME}:latest .
                '''
            }
        }

        stage('Push to GitHub Container Registry') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'ghcr-token', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                    sh '''
                        echo $GIT_PASSWORD | docker login ${REGISTRY} -u $GIT_USERNAME --password-stdin
                        docker push ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER}
                        docker push ${REGISTRY}/${IMAGE_NAME}:latest
                        docker logout ${REGISTRY}
                    '''
                }
            }
        }
    }
}
