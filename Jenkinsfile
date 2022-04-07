pipeline {
    agent any
    stages {
        stage('Docker Build') {
            steps {
                echo 'Docker Build...'
                script {
                    dockerapp = docker.build("leandroschwab/odoo-gbear:${env.BUILD_ID}",
                        '-f ./Dockerfile .')
                }
            }
        }
        stage('Docker Push Image') {
            steps {
                echo 'Docker Push Image...'
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
    }
}
