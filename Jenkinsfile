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
	/*agent {//docker as image
		docker {
			image 'maven:3.9.8'
		}
	}*/
	environment {
		//Get paths of configured tool myDocker and myMaven
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage('Checkout'){
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Build"
				//Print enviroment variables
				echo "PATH -$PATH"
				echo "BUILD_NUMBER -$env.BUILD_NUMBER"
				echo "BUILD_ID -$env.BUILD_ID"
				echo "JOB_NAME -$env.JOB_NAME"
				echo "BUILD_TAG -$env.BUILD_TAG"
				echo "BUILD_URL -$env.BUILD_URL"
			}
		}
		stage('Compile'){
			steps {
				echo "Compile"
				sh "mvn clean compile"
			}
		}
		stage('Test'){
			steps {
				echo "Test"
				sh "mvn test"
			}
		}
		stage('Integration Test'){
			steps {
				echo "Integration Test"
				sh "mvn failsafe:integration-test failsafe:verify"
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

