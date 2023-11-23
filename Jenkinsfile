pipeline{
    agent any

    stages{
       stage("clone code"){
          steps{
             echo "cloning the code"
             git url:"https://github.com/KKhandale12/jenkins_declarative_pipekine.git", branch: "master"
        }

       }
       stage("build"){
          steps{
             echo "building the image"
              sh "docker-compose up -d"
            
            
        }

       }
       stage("push to docker hub"){
          steps{
             echo "pusing the image to dokcer hub"
             withCredentials([usernamePassword(credentialsId:"Docker_hub",passwordVariable:"dockerhubpass",usernameVariable:"dockerHubUser")]){
             sh "docker tag kk-note-app ${env.dockerHubUser}/kk-note-app:latest"
             sh "docker login -u ${env.dockerHubUser} -p ${env.dockerhubpass}" 
             sh "docker push ${env.dockerHubUser}/kk-note-app:latest" 
             } 
            
        }

       }
       stage("deploy"){
        steps{
           echo "deploying the container"
           sh "docker-compose down && docker-compose up -d"
            
        }

       }
    
        }
    
}
