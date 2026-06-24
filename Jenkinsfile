pipeline {
agent any

```
environment {
    IMAGE = "Iswarya/myapp"
}

stages {

    stage('Checkout') {
        steps {
            git 'https://github.com/iswarya602-lang/Project-kubectl.git'
        }
    }

    stage('Build Image') {
        steps {
            sh 'docker build -t $IMAGE:latest .'
        }
    }

    stage('Docker Login') {
        steps {
            withCredentials([usernamePassword(
                credentialsId: 'dockerhub',
                usernameVariable: 'USER',
                passwordVariable: 'PASS'
            )]) {
                sh '''
                echo $PASS | docker login -u $USER --password-stdin
                '''
            }
        }
    }

    stage('Push Image') {
        steps {
            sh 'docker push $IMAGE:latest'
        }
    }
}
```

}

       stage('Push Image') {
           steps {
               sh 'docker push $IMAGE:latest'
           }
       }

       stage('Deploy to EKS') {
           steps {
               sh 'kubectl apply -f deployment.yaml'
               sh 'kubectl apply -f service.yaml'
           }
       }
   }
}
