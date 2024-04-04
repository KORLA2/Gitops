pipeline {

    agent any
    
stages{
    stage('Clone repository') {
      
steps{
        checkout scm
}
    }

    stage('Build image') {
  steps{
      script{
          echo "Hello"
         withDockerRegistry(credentialsId: 'Dockercred',toolName:docker) {
   sh "docker build -t goutham2/pythonapp:lts ."
}
      }
  }
        
       
    }

    // stage('Test image') {
  

    //     app.inside {
    //         sh 'echo "Tests passed"'
    //     }
    // }

    stage('Push image') {
          steps{
      script{
         withDockerRegistry(credentialsId: 'Dockercred',toolName:docker) {
   sh 'docker push  goutham2/pythonapp:${env.BUILD_NUMBER} '
}
      }
  }
     
    }

    
    stage('Trigger ManifestUpdate') {
        steps{
                echo "triggering updatemanifestjob"
            
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
        }
}
}
