pipeline {
	// agent any 
	agent {
		docker {
			// image 'maven:3.9.8'
			image 'node:21.7'
		}
	}
	stages {
		stage('Build') {
			steps {
				// sh 'mvn --version'
				sh 'node --version'
				echo "Build"
			}
			post {
				always {
					echo 'I run at the end of the build stage'
				}
			}
		}
		stage('Test') {
			steps {
				echo "Test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
	}
	post { 
		always {
			echo 'I always run'
		}
		success {
			echo 'I run when successful'
		}
		failure {
			echo 'I run when failed'
		}
	}
}