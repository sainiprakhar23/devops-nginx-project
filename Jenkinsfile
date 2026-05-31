// Declarative Pipeline Syntax
pipeline {

    // Run pipeline on any available Jenkins agent/node
    agent any

    stages {

        // Stage 1: Verify Jenkins successfully executed the pipeline
        stage('Git Check') {

            steps {

                // Print message in Jenkins Console Output
                echo 'GitHub connected successfully'

            }
        }

        // Stage 2: Verify Jenkins can access Docker
        stage('Docker Check') {

            steps {

                // Run Windows command and show Docker version
                bat 'docker --version'

            }
        }

        // Stage 3: Build Docker Image
        stage('Build Docker Image') {

            steps {

                // Build image using Dockerfile present in repository root
                // -t = tag
                // nginx-devops = image name
                // v1 = image version/tag
                // . = current directory (contains Dockerfile)
                bat 'docker build -t nginx-devops:v1 .'

            }
        }
    }

    // Actions after pipeline completion
    post {

        // Executed only when all stages succeed
        success {

            echo 'Docker Image Built Successfully'

        }

        // Executed if any stage fails
        failure {

            echo 'Pipeline Failed'

        }
    }
}
