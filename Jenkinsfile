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

    stage('Checkout Source Code') {
      steps {
        echo "Checking out source code from GitHub"
        git branch: 'main',
            url: 'https://github.com/anandhinandhi052-web/demo-gitops-app.git'
      }
    }

    stage('Build & Push Image using Cloud Build') {
      steps {
        echo "Triggering Google Cloud Build"
        sh """
          gcloud config set project ${PROJECT_ID}
          gcloud builds submit --tag ${IMAGE_URI} .
        """
      }
    }

    stage('Verify Image in Artifact Registry') {
      steps {
        echo "Verifying image in Artifact Registry"
        sh """
          gcloud artifacts docker images list ${REGION}-docker.pkg.dev/${PROJECT_ID}/${REPO}
        """
      }
    }
  }

  post {
    success {
      echo "CI pipeline completed successfully. Image pushed to Artifact Registry."
    }
    failure {
      echo "CI pipeline failed. Please check logs."
    }
  }
}
