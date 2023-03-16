pipeline {
    agent any
    environment{
        DOCKERHUB_USENAME = "jobri237"
        IMAGE_TAG = "${env.BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USENAME}" + "/" + "ls-gitops"
        REGISTRY_CREDS = 'docker-hub'
    }
    
    stages {
        stage('Cleanup Workspace'){
            steps {
                script {
                    cleanWs()
                }
            }
        }

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
        }
        stage('Push image') {
            steps {
                script{
                    docker.withRegistry('', REGISTRY_CREDS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                            }
                        }
                    }
                }
        stage('Delete local image') {
                steps {
                    sh "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"
                    sh "docker rmi ${IMAGE_NAME}:latest" 
                }
            }
        
        stage('Trigger CD pipeline') {
            steps {
                build job: 'CD-PIPELINE', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
                
            }
        }
        
      }   
 }
