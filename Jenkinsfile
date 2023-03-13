pipeline {
  agent any
  stages {
    stage('checkout') {
      steps {
        script {
          pipeline {
            agent any

            environment {
              AZURE_SUBSCRIPTION_ID='99999999-9999-9999-9999-99999999'
              AZURE_TENANT_ID='99999999-9999-9999-9999-99999999'
              CONTAINER_REGISTRY='container registry name'
              RESOURCE_GROUP='resource group'
              REPO="repo name"
              IMAGE_NAME="image name"
              TAG="tag"
            }

            stages {
              stage('Example') {
                steps {
                  withCredentials([usernamePassword(credentialsId: 'myAzureCredential', passwordVariable: 'AZURE_CLIENT_SECRET', usernameVariable: 'AZURE_CLIENT_ID')]) {
                    sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
                    sh 'az account set -s $AZURE_SUBSCRIPTION_ID'
                    sh 'az acr login --name $CONTAINER_REGISTRY --resource-group $RESOURCE_GROUP'
                    sh 'az acr build --image $REPO/$IMAGE_NAME:$TAG --registry $CONTAINER_REGISTRY --file Dockerfile . '
                  }
                }
              }
            }
          }
        }

      }
    }

    stage('Build') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsId: 'myAzureCredential', passwordVariable: 'AZURE_CLIENT_SECRET', usernameVariable: 'AZURE_CLIENT_ID')]) {
            sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
            sh 'az account set -s $AZURE_SUBSCRIPTION_ID'
            sh 'az acr login --name $CONTAINER_REGISTRY --resource-group $RESOURCE_GROUP'
            sh 'az acr build --image $REPO/$IMAGE_NAME:$TAG --registry $CONTAINER_REGISTRY --file Dockerfile . '
          }
        }

      }
    }

  }
}