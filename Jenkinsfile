    pipeline {
        agent {
            docker { 
                label 'jenkins-agent'
                image 'node:16.14.2' 
            }
        }
        stages {
            stage('Install dependencies') {
                steps {
                    sh ' npm install'
                }
            }
            stage('Build App') {
                steps {
                    sh 'npm run build'
                }
            }
        }
    }
