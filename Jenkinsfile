pipeline {
  agent any

  environment {
    registry = 'https://registry.hub.docker.com'
    image = 'veek/alpine-php'
    registryCredential = 'dockerhub'
  }

  stages {
    stage('building PHP 7.2-dev') {
      steps {
        dir('base/7.2') {
          script {
            docker.withRegistry(registry, registryCredential) {
              def base = docker.build(image + ':7.2-dev')
              base.push()
            }
          }
        }
      }
    }

    stage('building PHP 7.2-dev-sf') {
      steps {
        dir('symfony/7.2') {
          script {
            docker.withRegistry(registry, registryCredential) {
              def base = docker.build(image + ':7.2-dev-sf', "-f Dockerfile.dev .")
              base.push()
            }
          }
        }
      }
    }

    stage('cleaning') {
      steps {
        cleanWs deleteDirs: true
      }
    }
  }
}
