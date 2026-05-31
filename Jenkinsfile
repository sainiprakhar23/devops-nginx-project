pipeline {


agent any

environment {

    // Docker Hub username
    DOCKER_USER = 'sainiprakhar23'

    // Docker image name
    IMAGE_NAME = 'nginx-devops'
}

stages {

    stage('Git Check') {

        steps {

            echo 'GitHub connected successfully'

        }
    }

    stage('Docker Check') {

        steps {

            bat 'docker --version'

        }
    }

    stage('Build Docker Image') {

        steps {

            // Build Docker image from Dockerfile
            bat 'docker build -t nginx-devops:v1 .'

        }
    }

    stage('Docker Login') {

        steps {

            withCredentials([
                usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )
            ]) {

                // Login to Docker Hub using Jenkins credentials
                bat '''
                docker login -u "%DOCKER_USERNAME%" -p "%DOCKER_PASSWORD%"
                '''

            }
        }
    }

    stage('Tag Docker Image') {

        steps {

            // Tag local image for Docker Hub
            bat '''
            docker tag nginx-devops:v1 sainiprakhar23/nginx-devops:v1
            '''

        }
    }

    stage('Push Docker Image') {

        steps {

            // Push image to Docker Hub
            bat '''
            docker push sainiprakhar23/nginx-devops:v1
            '''

        }
    }
}

post {

    success {

        echo 'Docker Image Built And Pushed Successfully'

    }

    failure {

        echo 'Pipeline Failed'

    }
}


}
