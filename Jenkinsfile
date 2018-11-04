pipeline {
  agent { label 'docker' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Build') {
      steps {
        docker.build("timgondasr/hellonode")
      }
    }
    stage('Publish') {
      when {
        branch 'master'
      }
      steps {
	        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
	            app.push("${env.BUILD_NUMBER}")
	            app.push("latest")
	        }
      }
    }
  }
}