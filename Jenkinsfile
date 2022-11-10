pipeline {
  agent none
    
  stages {
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

    stage('Execute uni tests') {
      agent {
        docker { 
          label 'jenkins-agent'
          image 'node:16.14.2'
        }
      }
      steps {
          sh 'npm run test'
      }
    }

    stage('Using SonarQube Containerized') {
      agent {
        label 'jenkins-agent'
      }
      steps {
        echo 'Scanning Code'
        sh "docker run --rm -e SONAR_HOST_URL='https://sonarcloud.io' -e SONAR_TOKEN='71976fc36105fa15501680e62729b95a0501ea4e' -e SONAR_SCANNER_OPTS='-Dsonar.organization=summit-test -Dsonar.projectKey=test-docker -Dsonar.javascript.lcov.reportPaths=./coverage/lcov.info' -v '/tmp/workspace/cattle-angular_main:/usr/src' sonarsource/sonar-scanner-cli"
      }
    }

    stage('Build App') {
      agent {
        docker { 
          label 'jenkins-agent'
          image 'node:16.14.2' 
        }
      }
      steps {
          sh 'npm run build'
      }
    }
  }
}
