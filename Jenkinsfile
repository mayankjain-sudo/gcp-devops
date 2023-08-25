pipeline {
    agent any
    stages {
        stage('Git checkout') {
            steps {
                // Clean before build
                cleanWs()
                checkout scm
            }
        }
        stage('Gcloud Install') {
            steps {
                // Checking gcloud 
                // sh '''
                //     curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-444.0.0-linux-x86_64.tar.gz
                //     tar -xf google-cloud-cli-444.0.0-linux-x86_64.tar.gz
                //     ./google-cloud-sdk/install.sh
                // '''

                script {
                    gcloudver=`gcloud --version > /dev/null`
                    if ( gcloudver == 0 ) {
                        sh "echo 'gcloud is already install'"
                    }  else {
                        sh "echo 'Hello from ${env.BRANCH_NAME} branch!'"
                    }
                    }
            }
        }
    }
}