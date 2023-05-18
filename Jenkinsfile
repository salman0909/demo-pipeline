pipeline {
    agent any
    environment {
        IMAGE='myjenkins-blueocean'
        TAG='2.387.3-1'
    }
    stages {
        stage('delete container') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerPassword', usernameVariable: 'dockerUsername')]) {
                    sh "docker container rm -f jenkins-blueocean"
                    sh "docker image rm -f myjenkins-blueocean:2.387.3-1"
                }
            }
        }
    }
}
