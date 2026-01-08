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

    stage('Checkout Code') {
      steps {
        echo "Code already checked out from GitHub"
      }
    }

    stage('Trigger Google Cloud Build') {
      steps {
        sh '''
          echo "Triggering Google Cloud Build..."
          gcloud builds submit \
            --tag $REGION-docker.pkg.dev/$PROJECT_ID/$REPO/$IMAGE:$TAG
        '''
      }
    }
  }
}
