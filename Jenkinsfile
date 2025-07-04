pipeline {
  agent any

  environment {
    PATH = "/usr/local/go/bin:$PATH"
    NEXUS_URL = "http://localhost:8082"
    REPO = "go-artifacts"
    ARTIFACT = "hello"
    VERSION = "v${BUILD_NUMBER}"
  }

  stages {
    stage('Git') {
      steps {
        git branch: 'main', url: 'https://github.com/64wolf95/sdvps-materials'
      }
    }

    stage('Build binary') {
      steps {
        sh 'CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo -o $ARTIFACT .'
      }
    }

    stage('Upload to Nexus') {
      steps {
        sh '''
          curl -u admin:Nexus-test --upload-file $ARTIFACT \
            $NEXUS_URL/repository/$REPO/$ARTIFACT-$VERSION
        '''
      }
    }
  }
}
