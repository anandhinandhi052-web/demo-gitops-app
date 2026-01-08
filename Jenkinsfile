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

    stage('Build Docker Image') {
      steps {
        sh '''
          echo "Building Docker image..."
          docker build -t $REGION-docker.pkg.dev/$PROJECT_ID/$REPO/$IMAGE:$TAG .
        '''
      }
    }

    stage('Authenticate to GCP Artifact Registry') {
      steps {
        sh '''
          echo "Authenticating Docker with GCP..."
          gcloud auth configure-docker $REGION-docker.pkg.dev -q
        '''
      }
    }

    stage('Push Image') {
      steps {
        sh '''
          echo "Pushing image to Artifact Registry..."
          docker push $REGION-docker.pkg.dev/$PROJECT_ID/$REPO/$IMAGE:$TAG
        '''
      }
    }
  }
}
