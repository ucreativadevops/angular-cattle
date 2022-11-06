pipeline {
    agent {
        docker { 
            label 'docker-ubuntu'
            image 'node:16.14.2' 
        }
    }
    stages {
        stage('Install dependencies') {
            steps {
                bat ' npm install'
            }
        }
        stage('Build App') {
            steps {
                bat 'npm run build'
            }
        }
    }
}