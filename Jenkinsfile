pipeline {
    agent any

    stages {
        stage('Check Docker') {
            steps {
                sh 'docker --version'
                sh 'docker info'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '407337d2-dbd1-4eda-82eb-93d4fe5f1b18', toolName: 'Docker', url: 'https://index.docker.io/v1/') {
                        sh 'chmod +x build.sh'
                        sh './build.sh'
                        if (env.GIT_BRANCH == "origin/dev") {
                            sh 'docker tag nginx-app gayatridevops11/finalapp_dev:latest'
                        } else if (env.GIT_BRANCH == "origin/main") {
                            sh 'docker tag nginx-app gayatridevops11/finalapp_prod:latest'
                        }
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '407337d2-dbd1-4eda-82eb-93d4fe5f1b18', toolName: 'Docker', url: 'https://index.docker.io/v1/') {
                        if (env.GIT_BRANCH == "origin/dev") {
                            sh 'docker push gayatridevops11/finalapp_dev:latest'
                        } else if (env.GIT_BRANCH == "origin/main") {
                            sh 'docker push gayatridevops11/finalapp_prod:latest'
                        }
                    }
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '407337d2-dbd1-4eda-82eb-93d4fe5f1b18', toolName: 'Docker', url: 'https://index.docker.io/v1/') {
                        sh 'chmod +x deploy.sh'
                        sh './deploy.sh'
                    }
                }
            }
        }
    }
}
