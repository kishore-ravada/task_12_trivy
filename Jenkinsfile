pipeline {

```
agent any

environment {
    IMAGE_NAME = 'task_12_springboot'
}

stages {

    stage('Checkout') {
        steps {
            checkout scm
        }
    }

    stage('Build Maven') {
        steps {
            sh 'mvn clean package'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t ${IMAGE_NAME} .'
        }
    }

    stage('Trivy Scan') {
        steps {
            sh '''
            trivy image \
              --severity CRITICAL \
              --exit-code 1 \
              ${IMAGE_NAME}
            '''
        }
    }

}

post {
    success {
        echo 'Build and Trivy scan successful'
    }
    failure {
        echo 'Pipeline failed because CRITICAL vulnerabilities were found'
    }
}
```

}
