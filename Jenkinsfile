pipeline {
	agent any 
	environment {
		dockerHome = tool "myDocker"
		mavenHome = tool "myMaven"
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	// agent {
	// 	docker {
	// 		// image 'maven:3.9.8'
	// 		image 'node:21.7'
	// 	}
	// }
	stages {
		stage('Checkout') {
			steps {
				sh 'mvn --version'
				sh 'docker --version'
				// sh 'node --version'
				echo "Build"
				echo "Path: $PATH"
				echo "Build Number: $env.BUILD_NUMBER"
				echo "Build ID: $env.BUILD_ID"
				echo "Build Tag: $env.BUILD_TAG"
				echo "Build URL: $env.BUILD_URL"
				echo "Job Name: $env.JOB_NAME"
			}
			post {
				always {
					echo 'I run at the end of the build stage'
				}
			}
		}
		stage('Compile') {
			steps {
				sh "mvn clean compile"
			}
		}
		stage('Test') {
			steps {
				sh "mvn test"
			}
		}
		stage('Integration Test') {
			steps {
				echo "Integration Test"
			}
		}
		stage('Package') {
			steps {
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image') {
			steps {
				// "docker build -t emilesherrott/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage = docker.build("docker build -t emilesherrott/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
		stage('Push Docker Image'){
			steps {
				script {
					docker.withRegistry('', 'dockerhub') {
						dockerImage.push()
						dockerImage.push('latest')
					}

				}
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