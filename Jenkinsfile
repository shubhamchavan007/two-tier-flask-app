pipeline{
    agent {label 'dev-agent'};
    stages{
        stage("code"){
            steps{
                echo "this is code stage"
                git url: "https://github.com/shubhamchavan007/two-tier-flask-app", branch: "master"
            }
        }
        stage("build"){
            steps{
                echo "this is build stage"
                sh "docker build -t two-tier-flaskapp ."
            }
        }
        stage("docker hub"){
            steps{
                echo "this is build stage"
                script{
                withCredentials([usernamePassword(credentialsId: "dockerHubCreds",
                usernameVariable:"dockerHubUser",
                passwordVariable:"dockerHubPass"
                )]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker image tag two-tier-flaskapp ${env.dockerHubUser}/two-tier-flaskapp:lates"
                    sh "docker push ${env.dockerHubUser}/two-tier-flaskapp:latest"
                }
                }
            }
        }
        stage("test"){
            steps{
                echo "this is test stage"
            }
        }
        stage("deploy"){
            steps{
                echo "this is deploy stage"
                sh "docker compose up -d"
            }
        }
        post{
            success{
                script{
                    emailext from:"sc2421999@gmail.com",
                        to: "sc2421999@gmail.com",
                        subject: "about build",
                        body: "the build was success"
                }
             }
            failure{
                script{
                          emailext from:"sc2421999@gmail.com",
                        to: "sc2421999@gmail.com",
                        subject: "about build",
                        body: "the build failed"
                }
             }
        }
    }
}
