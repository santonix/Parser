def imageName = 'mlabouardy/movies-parser'

pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build and Test') {
            steps {
                script {
                    def imageTest = docker.build("${imageName}-test", "-f Dockerfile.test .")
                    imageTest.inside {
                        sh 'golint'
                        sh 'go test'
                    }
                }
            }
        }
    }
}
