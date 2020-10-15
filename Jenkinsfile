pipeline {

  environment {
    registry = "192.168.0.133:5000"
    dockerImage = ""
  }

  agent any

  stages {

 
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "mykubeconfig")
        }
      }
    }

  }

}
