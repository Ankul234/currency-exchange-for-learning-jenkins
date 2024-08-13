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
	}
}

