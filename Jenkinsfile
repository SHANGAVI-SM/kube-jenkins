node {

    stage("Git Clone"){

        git credentialsId: 'Git_Hub', url: 'https://github.com/praveen1994dec/EKS_DEPLOYMENT.git', branch: 'main' 
    }

     stage("Build") {

       sh 'docker-compose up -d'
       sh 'docker images'

    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u shangavism -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push shangavism/kube-jenkins:latest'
    }

    stage("kubernetes deployment"){
        steps{
            
            sh 'kubectl config use-context minikube --insecure-skip-tls-verify'
            sh 'kubectl apply -f deployment.yml --context minikube'
        }
        
    }
}
