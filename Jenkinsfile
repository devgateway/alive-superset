pipeline {
  agent any

  environment {
    IMAGE_NAME = "alive-registry.dgstg.org/alive/superset"
    DOCKER_REGISTRY = "https://alive-registry.dgstg.org/"
  }

  stages {
    stage('build and push') {
      agent {
        label 'docker'
      }
      steps {
        script {
          IMAGE_TAG = env.GIT_COMMIT.take(5)

          docker.withRegistry(DOCKER_REGISTRY, "alive-registry-credentials") {
            sh "docker buildx build --push --target alive -t ${IMAGE_NAME}:${IMAGE_TAG} ."
          }
        }
      }
    }
  }
}
