pipeline {
  agent none
    
  stages {
    stage('Using SonarQube Containerized') {
      agent {
        label 'jenkins-agent'
      }
      steps {
        echo 'Scanning Code'
        sh 'docker run --rm -e SONAR_HOST_URL="https://sonarcloud.io" -e SONAR_SCANNER_OPTS="-Dsonar.projectKey=test-docker -Dsonar.organization=summit-test -Dsonar.sources=src" -v ".:/usr/src" sonarsource/sonar-scanner-cli'
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
