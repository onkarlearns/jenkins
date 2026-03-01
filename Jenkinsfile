pipeline {
  agent any
  stages {
    stage('Checkout code') {
      steps {
        git(url: 'https://github.com/onkarlearns/jenkins.git', branch: 'main')
      }
    }

    stage('Install and Build') {
      steps {
        node(label: 'Install and Build') {
          sh 'npm install'
          sh 'npm run build'
        }

      }
    }

  }
}