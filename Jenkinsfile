pipeline {

	agent any

	stages {

		stage ('TEST') {
			steps {
				echo "Test"
			}
		}

		stage ('Docker Build') {
			steps {
				sh 'docker build -t cicd-project-kube-1 .'
				sh 'docker tag cicd-project-kube-1 naverdocker/cicd-project-kube-1:latest'
				sh 'docker tag cicd-project-kube-1 naverdocker/cicd-project-kube-1:${BUILD_NUMBER}'
			}
		}
		
		stage ('Docker Publish') {
			steps {
				withCredentials([usernameColonPassword(credentialsId: 'dockerhub_cred', variable: 'dockerhub-pass')]) {
    					sh 'docker login -u naverdocker -p ${dockerhub-pass}'		
				}
				sh 'docker push naverdocker/cicd-project-kube-1:latest'
				sh 'docker push naverdocker/cicd-project-kube-1:${BUILD_NUMBER}'
			}
		}
	}
}	
												
		

