pipeline {
  agent any
  stages {
    stage('Code checkout') {
      parallel {
        stage('Code checkout') {
          steps {
            git(url: 'https://github.com/octopus237', branch: 'main')
          }
        }

        stage('install git') {
          steps {
            sh '''sudo apt update 
&&  sudo apt install git'''
          }
        }

      }
    }

  }
}