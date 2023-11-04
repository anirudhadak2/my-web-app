pipeline {
    agent  any
        stages{
        stage("Git Clone"){
            steps{
                git url: "https://github.com/anirudhadak2/my-web-app.git", branch: "main"
            }
        }
        stage("Create Docker Image"){
            steps{
		echo "Build and Test"
		withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
		sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker build -t webapp ."
		}
            }
        }
         stage("Push DockerImage to DockrHub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker images"
                sh "docker tag  webapp  anirudhadak2/new-app:webapp"
		sh "docker push anirudhadak2/new-app:webapp"
		}
	    }
	}
        stage("Deploy Using DOcker Compose"){
            steps{   
		 sh "docker-compose down && docker-compose up -d"           
                }
            }
        }
    }
