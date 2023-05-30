pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clonar el repositorio del proyecto
                git 'https://github.com/CliberCastillo/votacion.git'
            }
        }

        stage('Restore') {
            steps {
                // Restaurar las dependencias del proyecto .NET Core
                sh 'dotnet restore'
            }
        }
    }

    post {
        success {
            // Notificar el éxito del pipeline a un canal de Slack
            slackSend channel: '#alertas', message: "El pipeline de despliegue de .NET Core ha sido exitoso."
        }

        failure {
            // Notificar la falla del pipeline a un canal de Slack
            slackSend channel: '#alertas', message: "¡El pipeline de despliegue de .NET Core ha fallado!"
        }
    }
}
