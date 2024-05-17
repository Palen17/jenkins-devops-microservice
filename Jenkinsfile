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
	//agent any
	//agent{ docker { image 'maven:3.6.3'} }
	agent { docker { image 'node:21.7.3'} }
	stages{
		stage('Build') {
			steps{
				//sh 'mvn --version'
				sh 'node --version'
				echo "Build"
			}
		}
		stage('Test') {
			steps{
				echo "Test"
				
			}
		}
		stage('Integration Test') {
			steps{
				echo "Integration Test"
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