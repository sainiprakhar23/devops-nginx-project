pipeline {


agent any

environment {

    // Docker Hub username
    DOCKER_USER = 'sainiprakhar23'

    // Docker image name
    IMAGE_NAME = 'nginx-devops'

    // Jenkins build number used as image tag
    IMAGE_TAG = "${BUILD_NUMBER}"

    // Minikube kubeconfig location
    KUBECONFIG = 'C:\\Users\\saini\\.kube\\config'
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

            bat '''
            docker build -t %DOCKER_USER%/%IMAGE_NAME%:%IMAGE_TAG% .
            '''

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

                bat '''
                docker login -u "%DOCKER_USERNAME%" -p "%DOCKER_PASSWORD%"
                '''

            }
        }
    }

    stage('Push Docker Image') {

        steps {

            bat '''
            docker push %DOCKER_USER%/%IMAGE_NAME%:%IMAGE_TAG%
            '''

        }
    }

    stage('Kubernetes Debug') {

        steps {

            bat '''
            set KUBECONFIG=C:\\Users\\saini\\.kube\\config
            kubectl get nodes
            '''

        }
    }

    stage('Deploy To Kubernetes') {

        steps {

            bat '''
            set KUBECONFIG=C:\\Users\\saini\\.kube\\config
            kubectl set image deployment/nginx-deployment nginx=%DOCKER_USER%/%IMAGE_NAME%:%IMAGE_TAG%
            '''

        }
    }

    stage('Wait For Rollout') {

        steps {

            bat '''
            set KUBECONFIG=C:\\Users\\saini\\.kube\\config
            kubectl rollout status deployment/nginx-deployment
            '''

        }
    }
}

post {

    success {

        echo 'CI/CD Pipeline Completed Successfully'

    }

    failure {

        echo 'Pipeline Failed'

    }
}


}
