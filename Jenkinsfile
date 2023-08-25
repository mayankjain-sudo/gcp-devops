pipeline {
    agent any
    stages {
        stage('Git checkout') {
            steps {
                // Clean before build
                //cleanWs()
                checkout scm
            }
        }
        stage('Build') {
            steps {
                withCredentials([file(credentialsId: 'gcpLearning', variable: 'GC_KEY')]) {
                // Checking gcloud 
                    sh '''
                        gcloud auth activate-service-account --key-file=${GC_KEY}
                        #curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-444.0.0-linux-x86_64.tar.gz
                        #tar -xf google-cloud-cli-444.0.0-linux-x86_64.tar.gz
                        #./google-cloud-sdk/install.sh -q
                        #source ./google-cloud-sdk/path.bash.inc
                        gcloud --version
                        gcloud storage ls
                    
                '''
                }
            }
        }
    }
}
