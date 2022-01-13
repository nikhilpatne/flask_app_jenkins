pipeline {
  environment {
        registry = "harshadadeokar"
        DOCKERHUB_CREDENTIALS=credentials('docker')
        dockerImage = ''
        Name = "harshadadeokar/flask_image"
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'http://gsgit.gslab.com/deokarharshada/simpleflaskapp.git'
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build Name
        }
      }
    }
    stage('Publish image to Docker Hub') {
          
            steps {
        withDockerRegistry([ credentialsId: "docker", url: "" ]) {
          sh  'docker push harshadadeokar/flask_image:latest'
         
        }
                  
          }
        }
    stage('Docker Run') {
        steps {
          script {
               sh "docker rm app --force"
            dockerImage.run(" -p 5000:5000 --rm --name app")
          }
        }

    }

  }
}
