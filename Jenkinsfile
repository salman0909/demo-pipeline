pipeline {
    agent any
    environment {
        IMAGE='myjenkins-blueocean'
        TAG='2.387.3-1'
    }
    stages {
        stage('Build') {
            steps {
                sh "docker build --pull -t ${IMAGE}:${TAG} ."
            }
        }
        stage('create a container') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerPassword', usernameVariable: 'dockerUsername')]) {
                    sh """docker run \
                       --name jenkins-blueocean \
                       --restart=on-failure \
                       --detach \
                       --network jenkins \
                       --env DOCKER_HOST=tcp://docker:2376 \
                       --env DOCKER_CERT_PATH=/certs/client \
                       --env DOCKER_TLS_VERIFY=1 \
                       --publish 8090:8080 \
                       --volume jenkins-data:/var/jenkins_home \
                       --volume jenkins-docker-certs:/certs/client:ro \
                       myjenkins-blueocean:2.387.3-1"""
                }
            }
        }
    }
}
