// Declarative //
pipeline {
	agent any
	stages {
		stage('Test') {
			steps {
				echo 'Start Testing..'

				script {

					// call Pega to run the automated unit tests
					//def response = httpRequest authentication: 'Admin.RestbucksFW', consoleLogResponseBody: true, httpMode: 'POST', outputFile: 'ResponseOutput', responseHandle: 'NONE', url: 'http://l33153wus.rpega.com:8081/prweb/PRRestService/PegaUnit/Rule-Test-Unit-Case/pzExecuteTests?AccessGroup=RestbucksFW%3AAdministrators'
					//def response = httpRequest authentication: 'Admin.RestbucksFW', consoleLogResponseBody: true, httpMode: 'POST', responseHandle: 'NONE', url: 'http://l33153wus.rpega.com:8081/prweb/PRRestService/PegaUnit/Rule-Test-Unit-Case/pzExecuteTests?AccessGroup=RestbucksFW%3AAdministrators'
					def response = httpRequest authentication: '60e0ce3a-63a7-46fd-8964-c8ab04bf94dc', consoleLogResponseBody: true, httpMode: 'POST', outputFile: 'ResponseOutput.xml', responseHandle: 'NONE', url: 'http://l33153wus.rpega.com:8081/prweb/PRRestService/PegaUnit/Rule-Test-Unit-Case/pzExecuteTests?AccessGroup=RestbucksFW%3AAdministrators'
					echo "the status value = ${response.status}"

					// get the content
					String content = response.content
					//echo "the content value = ${content}"

					// see if the content contains "Failed"
					if ( content.contains("Failed") ) {
						echo "Failed found; therefore, all tests were NOT successful!!!"
					} else {
						echo "Failed not found; therefore, all tests were successful!!!"
					}

					// publish the JUnit test results
					junit '**/*.xml'

				}

				echo 'End Testing..'
			}
		}
		stage('Build') {
			steps {
				echo 'Building..'
			}
		}
		stage('Deploy') {
			steps {
				echo 'Deploying....'
			}
		}
	}
	post {
	    always {
	        echo 'Done - with success'
	        //mail to: 'francois_dobson@yahoo.com', subject: 'The Pipeline succeeded', body: 'The pipeline was successful'
	    }
	    failure {
	        echo 'Done - with error'
	        //mail to: 'francois_dobson@yahoo.com', subject: 'The Pipeline failed', body: 'The pipeline was NOT successful'
	    }
	}
}
