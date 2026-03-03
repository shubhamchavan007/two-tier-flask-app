pipeline{
    agent any;
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
                sh "docker build -t my-app ."
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
    }
}
