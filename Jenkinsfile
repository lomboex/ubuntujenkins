pipeline {
    agent any
{
    stages {
        stage('Limpiar Workspace') {
            steps {
                deleteDir() // Limpia todo antes de empezar
            }
        }
    
    stages {
        stage('Iniciar contenedor Ubuntu') {
            steps {
                script {
                    echo "Creando contenedor desde imagen ubuntu"
                    sh '''
                    docker pull ubuntu
                    docker run --name test-ubuntu -d ubuntu sleep 60
                    '''
                }
            }
        }

        stage('Instalar curl') {
            steps {
                script {
                    echo "Instalando curl dentro del contenedor"
                    sh 'docker exec test-ubuntu apt update'
                    sh 'docker exec test-ubuntu apt install -y curl'
                }
            }
        }

        stage('Verificar instalación') {
            steps {
                script {
                    echo "Verificando instalación de curl"
                    sh 'docker exec test-ubuntu curl --version'
                }
            }
        }

        stage('Limpiar') {
            steps {
                script {
                    echo "Eliminando contenedor"
                    sh 'docker rm -f test-ubuntu'
                }
            }
        }
    }
}

