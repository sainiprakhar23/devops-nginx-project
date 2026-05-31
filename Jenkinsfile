pipeline {
    agent any

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

    }
}
