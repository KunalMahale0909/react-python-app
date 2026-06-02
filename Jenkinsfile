pipeline {
agent any

environment {
    REGISTRY = "192.168.56.12/demo"
}

stages {

    stage('Build Backend') {
        steps {
            sh 'docker build -t $REGISTRY/backend:latest backend/'
        }
    }

    stage('Build Frontend') {
        steps {
            sh 'docker build -t $REGISTRY/frontend:latest frontend/'
        }
    }

    stage('Harbor Login') {
        steps {
            sh 'docker login 192.168.56.12 -u admin -p Harbor12345'
        }
    }

    stage('Push Backend') {
        steps {
            sh 'docker push $REGISTRY/backend:latest'
        }
    }

    stage('Push Frontend') {
        steps {
            sh 'docker push $REGISTRY/frontend:latest'
        }
    }

    stage('Deploy') {
        steps {
            sh 'kubectl apply -f k8s/backend-deployment.yaml'
            sh 'kubectl apply -f k8s/frontend-deployment.yaml'
        }
    }
}

}