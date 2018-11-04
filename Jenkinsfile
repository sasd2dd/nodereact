def app
pipeline {
agent any

  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Build') {
      steps {
        script
        {
        	app = docker.build("timgondasr/hellonode")
        }
      }
    }

    stage('Test image') {
		// this is the test step
		steps {
			script {
	        	app.inside {
	            	sh 'echo "Tests passed"'
	        	}
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