pipeline {
agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    script{
        def app
    }

    stage('Build') {
      steps {
        script
        {
        	app = docker.build("timgondasr/hellonode")
        }
      }
    }
    stage('Publish') {
      steps {
	        script{
				docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
	            	app.push("${env.BUILD_NUMBER}")
	            	app.push("latest")
	        	}
	        }
      }
    }
  }
}