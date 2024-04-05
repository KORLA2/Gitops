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
                  withDockerRegistry(credentialsId: 'Dockercred',toolName:Docker) {
 sh "docker build -t goutham2/app:lts ."
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
                  withDockerRegistry(credentialsId: 'Dockercred',toolName:Docker) {
 sh "docker push  goutham2/app:lts"
}
               }
           } 
        }
        
    
    
    // stage('Trigger ManifestUpdate') {
    //             echo "triggering updatemanifestjob"
    //             build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
    //     }
}
}
