node {

    stage("Git Clone"){

        git credentialsId: 'Git_Hub', url: 'https://github.com/praveen1994dec/EKS_DEPLOYMENT.git', branch: 'main' 
    }

     stage("Build") {

       sh 'docker build . -t shangavism/kube-jenkins:latest'
       sh 'docker image list'

    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u shangavism -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push shangavism/kube-jenkins:latest'
    }

    stage("kubernetes deployment"){
        sh 'kubectl apply -f deployment.yml --context minikube'
    }
}
