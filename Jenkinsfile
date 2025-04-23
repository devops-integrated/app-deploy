pipeline {
    agent any

    environment {
        IMAGE = "your-dockerhub-username/my-app:latest"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                // This step will build the Docker image
                sh 'docker build -t $IMAGE .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker push $IMAGE
                    '''
                }
            }
        }
    }
}
