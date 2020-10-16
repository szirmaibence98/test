pipeline {
  agent any

  environment {
    registry = '192.168.0.133:5000/justme/myweb'
    dockerImage = ''
    PROJECT_ID = 'PROJECT-ID'
    LOCATION = 'CLUSTER-LOCATION'
    CREDENTIALS_ID = 'gke'
    CLUSTER_NAME_TEST = 'CLUSTER-NAME-1'
    CLUSTER_NAME_PROD = 'CLUSTER-NAME-2'
  }





  stages {



    stage('Back-end') {
        steps {
            sh 'mvn --version'
        }
    }

    stage('Front-end') {
        steps {
            sh 'node --version'
        }
    }


    stage('kubernetes') {
        steps {
            sh 'kubectl get all'
        }
    }







    stage('Checkout Source') {
      steps {
        git(url: 'https://github.com/szirmaibence98/test.git', branch: 'main')
      }
    }



    stage('Build image') {
      steps {
        script {
          myapp = docker.build("szirmaibence98/jenkins:${env.BUILD_ID}")
        }

      }
    }



  stage("Push image") {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                            myapp.push("latest")
                            myapp.push("${env.BUILD_ID}")
                    }
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