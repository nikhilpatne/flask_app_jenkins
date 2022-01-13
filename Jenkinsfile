pipeline {
  agent packer_node
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/nikhilpatne/flask_app_jenkins.git'
      }
    }
    stage('Building image') {
      steps{
        sh 'docker build -t nickpatne/flask_image:latest .'
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
