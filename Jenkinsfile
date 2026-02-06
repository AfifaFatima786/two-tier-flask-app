pipeline{
    
    agent { label "dev"};
    stages{
        stage("Code"){
            steps{
                git url : "https://github.com/AfifaFatima786/two-tier-flask-app.git" , branch: "master"
                echo "Code clone hogya"
            }
        }
        stage("Build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }
        
        stage("Push to Hub"){
            steps{
                withCredentials([usernamePassword(
                credentialsId:"dockerHubCreds",
                passwordVariable: "dockerHubPass",
                usernameVariable: "dockerHubUser"
                )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag two-tier-flask-app ${env.dockerHubUser}/two-tier-flask-app:latest"
                sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
            }}
        }
        
        stage("Test"){
            steps{
                sh "echo y tmhara kaam ni h"
            }
        }
        
        
        stage("Deploy"){
            steps{
                sh "docker compose up -d"
            }
        }
    
    }
}
