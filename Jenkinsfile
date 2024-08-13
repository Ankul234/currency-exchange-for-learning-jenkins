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
				//compile the code (java)
				sh "mvn clean compile"
			}
		}
		stage('Test'){
			steps {
				echo "Test"
				//To run Unit Test
				//Files present inside src/test/java/com/
				sh "mvn test"
			}
		}//Test sample can be seen inside resources folder
		stage('Integration Test'){
			steps {
				echo "Integration Test"
				//Files present inside src/test/java/com/../cucumber
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
		//Build jar file
		stage('Package'){
			steps {
				echo "Package Jar"
				sh "mvn package -DskipTests"
			}
		}
		stage('Build Docker Image'){
			steps{
				//Primitive way
				//docker build -t ankul123/hello-world-python:$env.BUILD_TAG
			    //Declarative way
				script{
					dockerImage = docker.build("ankul123/hello-world-python:${env.BUILD_TAG}")
				}
			}
		}
		//Give credentials of docker to Jenkins
		//Jenkins page -> Credentials -> System -> Global credentials
		//-> Add Credentials -> enter username/password.
		// id and description -> dockerhub --> save
		stage('Push Docker Image'){
			steps{
				script{
					//Credentials added
					docker.withRegistry('','dockerhub'){
						dockerImge.push();
						dockerImage.push('latest');
					}
				}
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

