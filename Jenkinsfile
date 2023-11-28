pipeline {
    agent any

    environment {
        registryCredential = 'dockerhub'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    dir('file') {
                        version = sh(script: 'git rev-parse --short HEAD', returnStdout: true).trim()
                        sh "docker build -t sohaib2410/python-app:$version ."
                    }
                }
            }
        }

        stage('Publish') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        version = sh(script: 'git rev-parse --short HEAD', returnStdout: true).trim()
                        sh "docker push sohaib2410/python-app:$version"
                    }
                }
            }
        }
    }

}
