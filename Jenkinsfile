pipeline {


  environment {
    registry = "192.168.0.133:5000/justme/myweb"
    dockerImage = ""
  }



  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git url:'https://github.com/vamsijakkula/hellowhale.git', branch:'master'
      }
    }
    

      stage("Build image") {
            steps {
                script {
                    myapp = docker.build("vamsijakkula/hellowhale:${env.BUILD_ID}")
                }
            }
        }
    

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }


    
    stage('Deploy App') {
      steps {
        script {
          kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "kubeconfig")
        }
      }
    }

  }

}


