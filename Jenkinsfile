pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '407337d2-dbd1-4eda-82eb-93d4fe5f1b18', toolName: 'Docker', url: 'https://hub.docker.com/') {
                        sh 'chmod +x build.sh'
                        sh './build.sh'
                        if (env.GIT_BRANCH == "origin/dev") {
                            sh 'docker tag nginx-app gayatridevops11/finalapp-dev:latest'
                        } else if (env.GIT_BRANCH == "origin/main") {
                            sh 'docker tag nginx-app gayatridevops11/finalapp-prod:latest'
                        }
                    }
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '407337d2-dbd1-4eda-82eb-93d4fe5f1b18', toolName: 'Docker', url: 'https://hub.docker.com/') {
                        if (env.GIT_BRANCH == "origin/dev") {
                            sh 'docker push gayatridevops11/finalapp-dev:latest'
                        } else if (env.GIT_BRANCH == "origin/main") {
                            sh 'docker push gayatridevops11/finalapp-prod:latest'
                        }
                    }
                }
            }
        }
        stage('Deploy Docker Image') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '407337d2-dbd1-4eda-82eb-93d4fe5f1b18', toolName: 'Docker', url: 'https://hub.docker.com/') {
                        sh 'chmod +x deploy.sh'
                        sh './deploy.sh'
                    }
                }
            }
        }
    }
}
