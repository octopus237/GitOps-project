pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/octopus237/GitOps-project', branch: 'dev')
      }
    }

    stage('Build') {
      steps {
        sh '''
        stage(\'Build-docker-image\') {
            steps {
                withCredentials([usernamePassword(credentialsId: \'myAzureCredential\', passwordVariable: \'AZURE_CLIENT_SECRET\', usernameVariable: \'AZURE_CLIENT_ID\')]) {
                            sh \'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID\'
                            sh \'az account set -s $AZURE_SUBSCRIPTION_ID\'
                            sh \'az acr login --name $CONTAINER_REGISTRY --resource-group $RESOURCE_GROUP\'
                            sh \'az acr build --image $REPO/$IMAGE_NAME:$TAG --registry $CONTAINER_REGISTRY --file Dockerfile . \'
                        }
            }
      '''
        sh 'echo test'
      }
    }

  }
}