/*node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
	stage('Integration Test') {
		echo "Integration Test"
	}
}
*/
//Declarative
pipeline{
	agent any
	//agent{ docker { image 'maven:3.6.3'} }
	//agent { docker { image 'node:21.7.3'} }
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}

	stages{
		stage('Checkout') {
			steps{
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BULD_NUMBER"
				echo "BUILD_ID - $BUILD_ID"
				echo "JOB_NAME - $JOB_NAME"
				echo "BUILD_TAG - $BUILD_TAG"
				echo "BUILD_URL - $BUILD_URL"
			}
		}

		stage('Compile') {
			steps{
				sh "mvn clean compile"
			}
		}

		stage('Test') {
			steps{
				sh "mvn test"
				
			}
		}
		/*
		stage('Integration Test') {
			steps{
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}*/

		stage('Package'){
			steps{
				sh "mvn package -DskipTests"
			}
		}

		stage('Build docker image'){
			steps{
				//"docker build -t palen17/currency-exchange-devops:$BUILD_TAG"
				script{
					dockerImage = docker.build("palen17/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}

		stage('Push docker image'){
			steps{
				script{
					docker.withRegistry('', 'dockerhub1'){
						dockerImage.push()
						dockerImage.push('latest')
					}
				}
			}
		}
		
	} 
	post{
		always{
			echo 'I ran always'
		}
		success{
			echo 'Only run when success'
		}
		failure{
			echo 'Only run on fail'
		}
	}
	
}