pipeline {
  agent any

  environment {
    PATH = "/usr/local/go/bin:$PATH"
    REGISTRY = "localhost:8082"
    IMAGE = "hello-world"
    VERSION = "v${BUILD_NUMBER}"
  }

  stages {
    stage('Git') {
      steps {
        git branch: 'main', url: 'https://github.com/64wolf95/sdvps-materials'
      }
    }

    stage('Test') {
      steps {
        sh 'go test .'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build . -t $REGISTRY/$IMAGE:$VERSION'
      }
    }

    stage('Push') {
      steps {
        sh 'docker login $REGISTRY -u admin -p Nexus-test && docker push $REGISTRY/$IMAGE:$VERSION && docker logout'
      }
    }
  }
}
