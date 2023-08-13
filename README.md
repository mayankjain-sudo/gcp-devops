# gcp-devops

Learning GCP DevOps.

To build the custom image in GCP using packer follow the below steps before writing the packer code.
### Below steps creates an example Packer service account using gcloud. Cloud Build will impersonate Packer's service account to run Packer acting as a given service account.
	1. Set GCP project variables. Substitute my-project with your project identifier.
        exportPROJECT_ID=my-project
        exportPROJECT_NUMBER=`gcloud projects list --filter="$PROJECT_ID"--format="value(PROJECT_NUMBER)"`
	2. Create Service Account for Packer
	    gcloud iam service-accounts create packer --description "Packer image builder"
	3. Grant roles to Packer's Service Account
	    gcloud projects add-iam-policy-binding $PROJECT_ID\
            --role="roles/compute.instanceAdmin.v1"\
            --member="serviceAccount:packer@${PROJECT_ID}.iam.gserviceaccount.com"gcloud projects add-iam-policy-binding $PROJECT_ID --role="roles/iam.serviceAccountUser"\
            --member="serviceAccount:packer@${PROJECT_ID}.iam.gserviceaccount.com"
	4. Allow CloudBuild to impersonate Packer service account
	    gcloud iam service-accounts add-iam-policy-binding \
            packer@${PROJECT_ID}.iam.gserviceaccount.com \
            --role="roles/iam.serviceAccountTokenCreator"\
            --member="serviceAccount:${PROJECT_NUMBER}@cloudbuild.gserviceaccount.com"

Once above steps are completed then run cloudbuild.yaml file it will create docker packer image with entry point "/usr/bin/packer".

Now in ubuntu-image-example directory you will find aother cloudbuild.yaml which will use the image created in above step to build golden image using packer.
