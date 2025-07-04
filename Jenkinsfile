pipeline {
 agent any
 stages {
  stage('Git') {
   steps {git 'https://github.com/64wolf95/sdvps-materials'}
  }
  stage('Test') {
   steps {
    sh 'go test .'
   }
  }
  stage('Build') {
   steps {
    sh 'docker build . -t localhost:8082/hello-world:v$BUILD_NUMBER'
   }
  }
  stage('Push') {
   steps {
    sh 'docker login localhost:8082 -u admin -p Nexus-test && docker push localhost:8082/hello-world:v$BUILD_NUMBER && docker logout'   }
  }
 }
}
