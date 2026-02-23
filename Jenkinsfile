pipeline {
  agent none
  stages {
    stage('build and push') {
      agent {
        label 'docker'
      }
      steps {
        script {
          COMMIT_HASH = env.GIT_COMMIT.take(5)
          IMAGE_TAG = "4.1.1-${COMMIT_HASH}"

          docker.withRegistry("https://${env.DOCKER_REGISTRY_HOSTNAME}/", "alive-registry-credentials") {
            sh "docker buildx build --push --target alive -t ${env.DOCKER_REGISTRY_HOSTNAME}/alive/superset:${IMAGE_TAG} ."
          }
        }
      }
    }
  }
}
