pipeline {
    agent any
    
    stages {
        stage('Mostrar los contenedores corriendo') {
            steps {
                sh 'docker container ls'
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
        }
    }
} 
