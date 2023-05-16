pipeline {
    agent any
    
    environment{
        def imageTag
        def commitCode
    }
    stages {
        stage('Obtener rel Tag'){
            steps{
                script{
                    commitCode = sh(returnStdout: true, script: 'git log --pretty=format:%h -n 1').trim()
                    imageTag = "clibercastillo/votacion:${commitCode}"
                }
            }
        }
        stage('Mostrar los contenedores corriendo') {
            steps {
                sh 'docker container ls'
            }
        }
        stage('Docker Build'){
            steps{
                script{
                    sh 'docker build -t ${imageTag} .'
                }
            }
        }
        stege('Docker Run'){
            steps{
                sh 'docker run -d -p 8080:80 --name votacion-${commitCode} ${imageTag}'
            }
        }
        /*stage('dotnet version') {
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
