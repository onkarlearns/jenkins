pipeline {
  agent any
  stages {
    stage('Checkout code') {
      steps {
        git(url: 'https://github.com/onkarlearns/jenkins.git', branch: 'main')
      }
    }

    stage('check files avaible') {
      steps {
        sh 'ls -la'
      }
    }

  }
}