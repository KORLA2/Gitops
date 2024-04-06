pipeline {
agent any
stages{
    stage('Clone repository') {
      steps{
     checkout scm
    }
    }

    
//     stage('Build image') {

    
//            steps{
//                script{
//                   withDockerRegistry(credentialsId: 'Dockercred',toolName:'Docker') {
//  sh "docker build -t goutham2/app:${BUILD_NUMBER} ."
// }
//                }
//            } 
        
        
//     }

//     // stage('Test image') {
  

//     //     app.inside {
//     //         sh 'echo "Tests passed"'
//     //     }
//     // }

//     stage('Push image') {
//          steps{
//                script{
//                   withDockerRegistry(credentialsId: 'Dockercred',toolName:'Docker') {
//  sh "docker push  goutham2/app:${BUILD_NUMBER}"
// }
//                }
//            } 
//         }
        
    
    
    stage('Trigger ManifestUpdate') {
        steps{
            script{
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
            }
        }
        }
}
}
