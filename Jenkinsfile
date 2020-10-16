pipeline {
  agent any

  environment {
    registry = '192.168.0.133:5000/justme/myweb'
    dockerImage = ''
  }


  stages {
    stage('Checkout Source') {
      steps {
        git(url: 'https://github.com/szirmaibence98/test.git', branch: 'main')
      }
    }

    stage('Build image') {
      steps {
        script {
          myapp = docker.build("szirmaibence/myweb:${env.BUILD_ID}")
        }

      }
    }

    stage('Deploy App') {
      parallel {
        stage('Deploy App') {
          steps {
            script {
              kubernetesDeploy(configs: "myweb.yaml", kubeconfigId: "kubeconfig")
            }

          }
        }

   

      }
    }

  }

}