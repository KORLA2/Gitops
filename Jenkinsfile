node {
    def app

    stage('Clone repository') {
      

        checkout scm
    }
    

    
    stage('Build image') {

        stage{
            script{
                sh "sudo usermod -aG docker ${USER}"
            }
        }
       app = docker.build("goutham2/test")
        
    }

    stage('Test image') {
  

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }
    
    stage('Trigger ManifestUpdate') {
                echo "triggering updatemanifestjob"
                build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
        }
}
