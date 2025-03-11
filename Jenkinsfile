pipeline {
    agent any

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
                     sh 'docker tag dockerfile bolajidevops/my-nginx:1.0'
                     sh 'docker push bolajidevops/my-nginx:1.0'
                }
            }
        }
        stage ('Run Docker Container') {
           steps {
                script {
                     sh 'docker run -itd -p 8085:80 my-nginx:1.0'
                }
            }
        }            
