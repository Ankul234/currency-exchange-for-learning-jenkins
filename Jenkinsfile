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
	agent any//where build will run
	stages {
		stage('Build'){
			steps {
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
	}
}

