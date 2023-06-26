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
                anyOf {
                    branch 'master'
                    branch 'develop'
                }
            }
            steps {
                script {
                    def branchName = env.BRANCH_NAME
                    def publish = false

                    if (branchName == 'master') {
                        publish = true
                    }

                    // Build the website-builder image
                    sh 'docker build -t website-builder .'

                    // Publish the website on port 82 if 'publish' is true
                    if (publish) {
                        sh 'docker run -itd -p 82:80 --name=masterserver website-builder'
                    }
                }
            }
        }
    }
}


