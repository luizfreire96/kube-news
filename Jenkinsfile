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
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub'){
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
        stage("running aplication"){
            steps{
                script{
                    withKubeConfig([credentialsId: "kubeconfig"]){
                        sh "kubectl apply -f ./kubenews.yaml"
                    }
                }
            }
        }
    }
}