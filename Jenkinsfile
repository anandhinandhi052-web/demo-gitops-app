pipeline {
  agent any

  environment {
    PROJECT_ID = "static-concept-483605-s9"
    REGION     = "us-central1"
    REPO       = "demo-repo"
    IMAGE      = "demo-nginx"
    TAG        = "v1"
  }

  stages {

    stage('Build & Push Image (Cloud Build)') {
      steps {
        sh '''
          echo "Submitting build to Google Cloud Build..."

          gcloud builds submit \
            --tag $REGION-docker.pkg.dev/$PROJECT_ID/$REPO/$IMAGE:$TAG
        '''
      }
    }
  }
}
