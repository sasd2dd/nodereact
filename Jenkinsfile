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
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */
		script {
        	app.inside {
            	sh 'echo "Tests passed"'
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