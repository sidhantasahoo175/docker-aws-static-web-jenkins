pipeline {
    agent any

    environment {
        IMAGE = 'siddh342/docker-aws-static-web'
    }

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE:$BUILD_NUMBER -t $IMAGE:latest .'
            }
        }

        stage('Test Container') {
            steps {
                sh '''
                    docker rm -f ci-test 2>/dev/null || true
                    docker run -d --name ci-test -p 8081:80 $IMAGE:$BUILD_NUMBER
                    sleep 3
                    curl -f http://localhost:8081/
                    docker rm -f ci-test
                '''
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-credentials',
                    usernameVariable: 'DOCKERHUB_USER',
                    passwordVariable: 'DOCKERHUB_TOKEN'
                )]) {
                    sh '''
                        echo "$DOCKERHUB_TOKEN" | docker login -u "$DOCKERHUB_USER" --password-stdin
                        docker push $IMAGE:$BUILD_NUMBER
                        docker push $IMAGE:latest
                        docker logout
                    '''
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh '''
                    docker rm -f static-web 2>/dev/null || true
                    docker pull $IMAGE:latest
                    docker run -d --name static-web -p 8000:80 $IMAGE:latest
                '''
            }
        }
    }

    post {
        always {
            sh 'docker rm -f ci-test 2>/dev/null || true'
        }
    }
}