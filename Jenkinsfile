pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
               script {
                   withDockerRegistry(credentialsId: '9cb9951e-ace0-402a-a217-6ce5f94199d1', toolName: 'docker') {
                    sh 'chmod +x build.sh'
                    sh './build.sh'
                    sh 'docker tag nginx-app gayatridevops11/finalapp-dev:latest'
                }
                }
               }
        }
        stage('Deploy Docker Image') {
            steps {
               script {
                   withDockerRegistry(credentialsId: '9cb9951e-ace0-402a-a217-6ce5f94199d1', toolName: 'docker') {
                    sh 'docker push gayatridevops11/finalapp-dev:latest' 
                    sh 'chmod +x deploy.sh'
                    sh './deploy.sh'
                }
                }
            } 
        }
    }
}