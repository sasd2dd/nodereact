pipeline {
    agent {
        docker { 
        	image 'node:7-alpine'
        	args '-p 3000:3000'
         }
    }
    stages {
        stage('Version') {
            steps {
                sh 'node --version'
            }
        }
        stage('Install') {
            steps {
                sh 'npm install'
            }
        }
    }
}