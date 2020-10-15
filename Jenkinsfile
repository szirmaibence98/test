pipeline {
    agent any
    
    environment {
        // The MY_KUBECONFIG environment variable will be assigned
        // the value of a temporary file.  For example:
        //   /home/user/.jenkins/workspace/cred_test@tmp/secretFiles/546a5cf3-9b56-4165-a0fd-19e2afe6b31f/kubeconfig.txt
        MY_KUBECONFIG = credentials('kubeconfig')
    }
    stages {
        stage('Example stage 1') {
            steps {
                sh("kubectl --kubeconfig $KUBECONFIG get pods")
            }
        }
    }
}