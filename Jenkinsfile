pipeline {
    agent any
    environment{
        DOCKERHUB_USENAME = "jobri237"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USENAME}" + "/" + "${APP_NAME}"
        REGISTRY_CREDS = 'docker-hub'
    }

    stages {
        stage('Checkout to dev') {
            steps {
                git branch: 'dev', url: 'https://github.com/octopus237/GitOps-project'
            }
        }
        
        stage('Build image') {
            steps {
                script{
                    docker_image = docker.build "${IMAGE_NAME}"
                }
            }
        
        stage('Push image') {
            steps {
                script{
                    docker.withRegistry('', REGISTRY_CREDS) {
                        docker_image.push("${BUILD_NUMBER}")
                        docker_image.push('latest')
                            }
                        }
                    }
                }
            }
        }
    }
