pipeline {
    agent any

    stages('Construção da imagem'){
        stage('Checkout Source') {
            steps{
                script {
                    git branch: 'main',
                        credentialsId: 'Credential ID',
                        url: 'https://github.com/hubpagec/pass_generator.git'
                }
            }
        }

        stage('Build Docker image') {
            steps{
                script{
                    dockerapp = docker.build("192.168.3.138/devops/pass_generator:${env.BUILD}",
                        '-f ./Dockerfile .')
                }

            }
        }
        stage('Push Docker Image') {
            steps{
                script{
                    docker.withRegistry('http://192.168.3.138/devops', 'harbor'){
                        dockerapp.push('latest')
                        dockerapp.push("${env.BUILD_ID}")
                    }
                }
            }
        }
    }
}