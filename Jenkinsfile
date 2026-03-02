pipeline {
    agent any
    environment {
        REGISTRY = 'ghcr.io'
        IMAGE_NAME = 'onkarlearns/jenkins'
        REGISTRYCredentials = credentials('github-token')
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
                sh '''
                    echo ${REGISTRYCredentials} | docker login ${REGISTRY} -u onkarlearns --password-stdin
                    docker push ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER}
                    docker push ${REGISTRY}/${IMAGE_NAME}:latest
                    docker logout ${REGISTRY}
                '''
            }
        }
    }
}
