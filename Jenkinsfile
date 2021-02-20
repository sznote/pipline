pipeline  {
  environment {
    registry = "https://gitlab:5050"
	registryCredential = 'gitlab-registry'
	dockerImage='saza/sazademo/pip-image' + ":${BUILD_NUMBER}"
  }
  agent {
	node { label 'agent1' }
  }
  
  stages {
	stage('Cloneing git') {
	  steps {
	    git( url: 'https://github.com/sznote/pipline.git' ,
           branch: 'main' )
		}
	  }
    stage('Build image') {
	  steps{
	    script {
	      dcokerImage = docker.build dockerImage
	    }
	  }
	}
	
	stage('Pulling image'){
	  steps{
	    script {
		   docker.withRegistry(registry, registryCredential){
		      dcokerImage.push()
		   }
		}
	  }
	}
  
    stage('remove Unused docker image') {
	  steps{
	    sh "docker rmi $registry/$dockerImage"
	  }
  
    }
  }
}