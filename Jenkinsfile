pipeline {
  agent none
  stages {
    stage('Using SonarQube Containerized') {
      agent {
        docker {
          label 'jenkins-agent'
          image 'sonarsource/sonar-scanner-cli'
          args "-e SONAR_HOST_URL='https://sonarcloud.io' -e SONAR_SCANNER_OPTS='-Dsonar.projectKey=test-docker -Dsonar.organization=summit-test -Dsonar.sources=src' -v /tmp/workspace/cattle-angular_main:/usr/src"
          reuseNode true
        }
      }
      steps {
        echo 'Scanning Code'
        checkout scm
      }
    }
    stage('Install dependencies') {
      agent {
        docker { 
          label 'jenkins-agent'
          image 'node:16.14.2' 
          reuseNode true
        }
      }
      steps {
          sh 'npm install'
      }
    }
    stage('Build App') {
      agent {
        docker { 
          label 'jenkins-agent'
          image 'node:16.14.2' 
          reuseNode true
        }
      }
      steps {
          sh 'npm run build'
      }
    }
  }
}
