pipeline{
    agent any
    stages{
        stage("Build docker image"){
            steps{
                script{
                    dockerapp = docker.build("lafreire96/kube-news:${env.BUILD_ID}", "-f ./src/Dockerfile ./src")
                }
            }
        }
        stage("push docker iamge"){
            steps{
                script{
                    docker.withRegistry("https://registry.hub.docker.com", "1")
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")
                }
            }
        }
    }
}