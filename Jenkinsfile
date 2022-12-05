pipeline {

	agent any

	stages {
		stage ('Docker Build') {
			steps {
				sh 'docker build -t cicd-project-kube-1 .'
				sh 'docker tag cicd-project-kube-1 naverdocker/cicd-project-kube-1:latest'
				sh 'docker tag cicd-project-kube-1 naverdocker/cicd-project-kube-1:${BUILD_NUMBER}'
			}
		}
		stage ('Docker Publish') {
			steps {
				withCredentials([string(credentialsId: 'dockerhub_secret', variable: 'dockerhub_pass')]) {
    					sh "docker login -u naverdocker -p ${dockerhub_pass}"		
				}
				sh 'docker push naverdocker/cicd-project-kube-1:latest'
				sh 'docker push naverdocker/cicd-project-kube-1:${BUILD_NUMBER}'
			}
		}
		stage ('Deploy to Kubernetes') {
			steps {
				sh 'sudo kubectl apply -f /var/lib/jenkins/workspace/cicd-project-kube-1/pod.yaml'
				sh 'sudo kubectl rollout restart deployment dep-1'
			}
		} 
	}
}	

