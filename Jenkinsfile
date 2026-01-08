pipeline {
  agent any

  environment {
    PROJECT_ID = "static-concept-483605-s9"
    REGION     = "us-central1"
    REPO       = "demo-repo"
    IMAGE      = "demo-nginx"
    TAG        = "v1"

    IMAGE_URI  = "${REGION}-docker.pkg.dev/${PROJECT_ID}/${REPO}/${IMAGE}:${TAG}"
  }

  stages {

    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/<YOUR_GITHUB_USERNAME>/<YOUR_REPO>.git'
      }
    }

    stage('Authenticate to GCP') {
      steps {
        withCredentials([file(credentialsId: 'gcp-sa-key', variable: 'GCLOUD_KEY')]) {
          sh '''
            gcloud auth activate-service-account --key-file=$GCLOUD_KEY
            gcloud config set project static-concept-483605-s9
          '''
        }
      }
    }

    stage('Build & Push Image (Cloud Build)') {
      steps {
        sh '''
          gcloud builds submit --tag us-central1-docker.pkg.dev/static-concept-483605-s9/demo-repo/demo-nginx:v1 .
        '''
      }
    }

  }
}
