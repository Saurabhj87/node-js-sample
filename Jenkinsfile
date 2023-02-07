pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('jenkins-github')
  }
  stages {
    stage('Build') {
      steps {
        sh '/usr/bin/docker build -t saurabhj87/jenkins-docker-hub .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh '/usr/bin/docker push saurabhj87/jenkins-docker-hub'
      }
    }
  }
  post {
    always {
      sh '/usr/bin/docker logout'
    }
  }
}
