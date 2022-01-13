pipeline {
  environment {
        registry = "nickpatne"
        DOCKERHUB_CREDENTIALS=credentials('dockerhub')
        dockerImage = ''
        Name = "nickpatne/flask_image"
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/nikhilpatne/flask_app_jenkins.git'
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
        withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
          sh  'docker push nickpatne/flask_image:latest'
         
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
