pipeline {

```
agent any

environment {

    // Docker Hub username
    DOCKER_USER = 'sainiprakhar23'

    // Image name
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

            // Build image locally on Jenkins machine
            bat 'docker build -t nginx-devops:v1 .'

        }
    }

    stage('Docker Login') {

        steps {

            // Read credentials from Jenkins Credentials Store
            withCredentials([
                usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )
            ]) {

                bat '''
                echo %DOCKER_PASSWORD% | docker login -u %DOCKER_USERNAME% --password-stdin
                '''

            }
        }
    }

    stage('Tag Docker Image') {

        steps {

            bat '''
            docker tag nginx-devops:v1 sainiprakhar23/nginx-devops:v1
            '''

        }
    }

    stage('Push Docker Image') {

        steps {

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
```

}
