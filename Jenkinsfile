pipeline{
    agent any;
    stages{
        stage("code"){
            steps{
                echo "this is code stage "
                git url: "https://github.com/shubhamchavan007/two-tier-flask-app",branch: "master"
            }
            
        }
         stage("build"){
            steps{
                echo "this is code stage "
                sh "docker build -t two-tier-flaskapp ."
            }
            
        }
         stage("test"){
            steps{
                echo "this is code stage "
            }
            
        }
        stage("docker-push"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHubCreds",
                usernameVariable:"dockerHubUser",
                passwordVariable:"dockerHubPass")]){
              
             sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
             sh "docker image tag two-tier-flaskapp ${env.dockerHubUser}/two-tier-flaskapp"
             sh "docker push ${env.dockerHubUser}/two-tier-flaskapp:latest"
                }
                echo "this is to docker push to docker hub "
            }
            
        }
        
         stage("deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
                echo "this is code stage "
            }
            
        }
        
    }
}
