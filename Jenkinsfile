pipeline {
  agent none
  stages {
    stage('Using SonarQube Containerized') {
      docker {
        label 'jenkins-agent'
        image 'sonarsource/sonar-scanner-cli'
        args '-e SONAR_HOST_URL="https://sonarcloud.io" -e SONAR_SCANNER_OPTS="-Dsonar.projectKey=test-docker -Dsonar.organization=summit-test -Dsonar.sources=src" -v ".:/usr/src"'
      }
    }
    stage('Install dependencies') {
      agent {
        docker { 
          label 'jenkins-agent'
          image 'node:16.14.2' 
        }
      }
      steps {
          sh 'npm install'
      }
    }
    stage('Build App') {
        steps {
            sh 'npm run build'
        }
    }
  }
}
