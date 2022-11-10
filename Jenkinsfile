pipeline {
  agent {
    docker { 
      label 'jenkins-agent'
      image 'node:16.14.2' 
    }
  }
    
  stages {
    stage('Using SonarQube Containerized') {
      steps {
        echo 'Scanning Code'
        sh 'docker run --rm -e SONAR_HOST_URL="https://sonarcloud.io" -e SONAR_SCANNER_OPTS="-Dsonar.projectKey=test-docker -Dsonar.organization=summit-test -Dsonar.sources=src" -v "C:\Dev\Repos\angular-cattle:/usr/src" sonarsource/sonar-scanner-cli'
      }
    }
    stage('Install dependencies') {
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
