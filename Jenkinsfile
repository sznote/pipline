pipline {
  environment {
    registry = "https://gitlab:5050"
	registryCredential = 'gitlab-registry'
	dockerImage=saza/sazademo/pip-image + ":${BUID_NUMBER}"
  }
  agent {
	node { label 'agent1' }
  }
  
  stages {
	state('Cloneing git') {
	  step {
	    git( url: 'https://github.com/sznote/pipline.git' ,
           branch: 'main' )
		}
	  }
    stage('Build image') {
	  step{
	    script {
	      dcokerImage = docker.build dockerImage
	    }
	  }
	}
	
	stage('Pulling image'){
	  step{
	    scrtip{
		   docker.withRegistry(registry, registryCredential){
		      dcokerImage.push()
		   }
		}
	  }
	}
  
    state('remove Unused docker image') {
	  step{
	    sh "docker rmi $registry/$dockerImage
	  }
  
    }
  }
}