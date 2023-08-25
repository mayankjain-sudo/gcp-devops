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
                    def gcloudver = sh(script:"gcloud --version > 2>&1", returnStatus:true)
                    if ( $gcloudver == 0 ) {
                        sh "echo 'gcloud is already install'"
                    }  else {
                        sh "echo 'Install cloud'"
                    }
                    }
            }
        }
    }
}