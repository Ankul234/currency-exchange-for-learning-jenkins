//Scripted Pipeline Approach
/*node {
	stage('Build') {
		echo "Build"
	}
	stage('Test') {
		echo "Test"
	}
	//Stage can be removed as well
	echo "integration Test"
}
*/
//DECLAARATIVE PIPELINES
//Checkout SCM happens in it along with many other features
pipeline {
	//agent any//where build will run
	agent {//docker as image
		docker {
			image 'maven:3.9.8'
		}
	}
	stages {
		stage('Build'){
			steps {
				sh 'mvn --version'
				echo "Build"
			}
		}
		stage('Test'){
			steps {
				echo "Test"
			}
		}
		stage('Integration Test'){
			steps {
				echo "Integration Test"
			}
		}
	}//End of all stages
	//do something based on the status
	post {
		always {
			echo 'All stages completed : '
		}
		success {
			echo 'Hey Amit, Compiled successfully'
		}
		failure {
			echo 'Sorry Amit, Compilation failed'
		}
		//Other 2 status is
		//changed and unstable
	}
}

