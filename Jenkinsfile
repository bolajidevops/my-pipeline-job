pipeline {
    agent any
    environment {
        registry = 'bolajidevops/my-nginx'
        IMAGE_TAG = '1.0'
        DOCKERHUB_CREDENTIALS_ID = 'dockerhub_credentials'
        dockerImage = ''
        }
    
    stages {
        stage('Connect To Github') {
            steps {
                    checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/bolajidevops/my-pipeline-job.git']])
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t dockerfile .'
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker run -itd -p 8084:80 dockerfile'
                }
            }
        }
        stage ('Push Docker image') {
           steps {
                script {
                     sh 'docker tag dockerfile registry:IMAGE_TAG'
                     sh  'docker.withRegistry('', dockerhub_credentials)'
                     sh 'docker push registry:IMAGE_TAG'
                }
            }
        }
        stage ('Run Docker Container from dockerhub') {
           steps {
                script {
                     sh 'docker run -itd -p 8085:80 my-nginx:1.0'
                }
            }
        }
    }    
}    