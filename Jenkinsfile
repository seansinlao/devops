pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('seansinlao')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t seansinlao/devops .'
      }
    }
    stage('Login') {
  steps {
  sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push seansinlao/devops'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}

