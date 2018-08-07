def genericSh(cmd) {
  if (isUnix()) {
    sh cmd
  }
  else {
    bat cmd
  }
}

node {
  stage('Checkout') {
    checkout scm
  }

  stage('Build') {
    azureIoTEdgePush dockerRegistryType: 'common', dockerRegistryEndpoint: [credentialsId: 'docker', url: 'xshiacr.azurecr.io'], modulesToBuild: '*', azureCredentialId: 'azuresp', resourceGroup: 'xshi-demo-locked', rootPath: './'
  }

  stage('Deploy') {
    azureIoTEdgeDeploy azureCredentialsId: 'azuresp', deploymentId: 'jenkins-deploy', deploymentType: 'single', deviceId: 'iot-edge-prod', iothubName: 'xshi-demo-hub', priority: '0', resourceGroup: 'xshi-demo-locked', rootPath: './', targetCondition: ''
  }
}