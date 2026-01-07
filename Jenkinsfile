pipeline {
  agent any

  environment {
    PROJECT_ID = "static-concept-483605-s9"
    REGION = "us-central1"
    REPO = "demo-repo"
    IMAGE = "demo-nginx"
    TAG = "v1"
  }

  stages {

    stage('Checkout') {
      steps {
        git branch: 'main',
        url: 'https://github.com/anandhinandhi052-web/demo-gitops-app.git'
      }
    }

    stage('Build Image') {
      steps {
        sh '''
        docker build -t $REGION-docker.pkg.dev/$PROJECT_ID/$REPO/$IMAGE:$TAG .
        '''
      }
    }

    stage('Authenticate GCP') {
      steps {
        sh '''
        gcloud auth configure-docker $REGION-docker.pkg.dev -q
        '''
      }
    }

    stage('Push Image') {
      steps {
        sh '''
        docker push $REGION-docker.pkg.dev/$PROJECT_ID/$REPO/$IMAGE:$TAG
        '''
      }
    }

  }
}
