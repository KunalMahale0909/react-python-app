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
