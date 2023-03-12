pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/octopus237/GitOps-project', branch: 'dev')
      }
    }

  }
}