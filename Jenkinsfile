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
            steps{
                sh 'docker image ls'
            }
        }
        stage('Docker Build & Push') {
            steps{
                script{  
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
                        def appVotacion = docker.build("${imageTag}", ".")
                        appVotacion.push()
                    }
                }  
            }  
        }
        stages {
            stage('Build and Push Docker Image') {
                steps {
                    script {
                        def awsAccountId = 'tu-ID-de-cuenta-de-AWS'
                        def awsRegion = 'tu-región-de-AWS'
                        def ecrRepository = 'nombre-de-tu-repositorio-ECR'
                        def imageTag = 'etiqueta-de-la-imagen'
                    
                        // Iniciar sesión en ECR utilizando las variables de entorno
                        ecrLogin = sh(returnStdout: true, script: "aws ecr get-login-password --region ${env.AWS_REGION} | docker login --username AWS --password-stdin ${env.AWS_ACCOUNT_ID}.dkr.ecr.${env.AWS_REGION}.amazonaws.com")
                        // Subir la imagen a ECR
                        sh "docker push ${awsAccountId}.dkr.ecr.${awsRegion}.amazonaws.com/${imageTag}"
                    }
                }
            }
        }
        stage('Listado de Contenedores Final') {
            steps{
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
