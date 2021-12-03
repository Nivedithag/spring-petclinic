pipeline {
  environment {
    imagename = 'nivedithag/docker-123:java-docker'
    registryCredential = 'Dockerhub' 
  }
  agent any
  
  stages{
    stage('Cloning git repo'){
      steps {
        git([url: 'https://github.com/Nivedithag/spring-petclinic', branch: 'main'])
      }
    }
    stage ('Building image') {
      steps {
        script{
          dockerImage = docker.build imagename
        }
      }
    }
    stage ('Deploy Image') {
      steps {
        script{
          docker.withRegistry('', registryCredential){
            dockerImage.push('$BUILD_NUMBER')
            dockerImage.push('latest')
          }
        }
      }
    }
  }
}
