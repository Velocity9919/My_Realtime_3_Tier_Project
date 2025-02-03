pipeline {
    agent any
    
    tools{
        jdk 'jdk11'
        nodejs 'nodejs16'  
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Velocity9919/My_Realtime_Project.git'
            }
        }
        
        stage('backend application') {
            steps {
                dir('Application-Code/backend') {
                    sh "npm install" 

                }
            }
        }
        
        stage('frontend application') {
            steps {
                dir('Application-Code/frontend') {
                    sh "npm install"

                }
            }
        }

        stage("Docker backend Build & push") {
            steps {
                script {
                    dir('Application-Code/backend') {
                        withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker'){
                        
                            sh 'docker system prune -f'
                            sh 'docker container prune -f'
                            sh 'docker build -t three-tier-backend .'
                            sh "docker tag three-tier-backend nareshbabu1991/three-tier-backend:latest "
                            sh "docker push nareshbabu1991/three-tier-backend:latest "
                        }
                    }
                }
            }
        }

        stage("Docker frontend Build & push") {
            steps {
                script {
                    dir('Application-Code/frontend') {
                        withDockerRegistry(credentialsId: 'dockerhub', toolName: 'docker'){
                        
                            sh 'docker system prune -f'
                            sh 'docker container prune -f'
                            sh 'docker build -t three-tier-frontend .'
                            sh "docker tag three-tier-frontend nareshbabu1991/three-tier-frontend:latest "
                            sh "docker push nareshbabu1991/three-tier-frontend:latest "
                        }
                    }
                }
            }
        }
    }
}
