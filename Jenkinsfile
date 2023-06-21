pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/vibha1995/website.git'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -t website-builder .'
      }
    }

    stage('Publish') {
      when {
        branch 'master'
      }
      steps {
        sh 'docker run -d -p 82:80 --name website-container website-builder'
      }
    }
  }
}

