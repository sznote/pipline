node('agent1'){
  stage('build image'){
      
    checkout scm

    docker.withRegistry('https://gitlab:5050', 'gitlab-registry') {

    def dockerfile = 'Dockerfile'
    def customImage = docker.build("saza/sazademo/my-image:${env.BUILD_ID}", "-f ${dockerfile} .") 
     customImage.push()

    }
  
  }
}
