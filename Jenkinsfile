pipeline {
    agent any
    stages {
        stage('Setup Node.js') {
            steps {
                sh '''
                    if ! command -v node &> /dev/null; then
                        curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
                        sudo apt-get install -y nodejs
                    fi
                '''
            }
        }

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
    }
}
