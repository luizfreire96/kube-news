pipeline{
    agent any
    stages{
        stage("Build docker image"){
            steps{
                script{
                    dockerapp = docker.Build("lafreire96/kube-news:${env.BUILD_ID}", "-f ./src/Dockerfile ./src")
                }
            }
        }
    }
}