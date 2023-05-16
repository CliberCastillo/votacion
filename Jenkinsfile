pipeline {
    agent any
    
    environment{
        imageTag = ""
        commitCode = ""
    }
    stages {
        stage('Obtener el Tag'){
            steps{
                script{
                    commitCode = sh(returnStdout: true, script: 'git log --pretty=format:%h -n 1').trim()
                    imageTag = "clibercastillo/votacion:${commitCode}"
                }
            }
        }
        stage('Listado de Contenedores') {
            steps {
                sh 'docker image ls'
            }
        }
        stage('Docker Build & Push') {
            steps {
                script {  
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
                        def appVotacion = docker.build("${imageTag}", ".")
                        appVotacion.push()
                    }
                }  
            }  
        }
        stage('Listado de Contenedores') {
            steps {
                sh 'docker image ls'
            }
        }
        /*stage('Docker Build'){
            steps{
                sh "docker build -t ${imageTag} ."
            }
        }
        stage('Docker Run'){
            steps{
                sh "docker run -d -p 8092:80 --name votacion-${commitCode} ${imageTag}"
            }
        }
        stage('dotnet version') {
            steps {
                script {
                    def contenedorTest = docker.image('mcr.microsoft.com/dotnet/sdk:7.0')
                    contenedorTest.pull()
                    contenedorTest.inside {
                        sh 'dotnet --version'
                    }
                }
            }
        }*/
    }
} 
