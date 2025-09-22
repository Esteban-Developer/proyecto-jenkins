pipeline {
    agent any

    environment {
        DOCKER_HOST = "tcp://dind:2375"
    }

    stages {
        stage('Clonar código') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Esteban-Developer/proyecto-jenkins.git'
            }
        }

        stage('Verificar archivos') {
            steps {
                sh 'ls -l'
                sh 'cat index.html'
            }
        }

        stage('Desplegar página') {
            steps {
                script {
                    docker.withServer("tcp://dind:2375") {
                        sh '''
                          # Si existe un contenedor viejo, eliminarlo
                          docker rm -f miweb || true
                          
                          # Crear el contenedor con la carpeta completa montada
                          docker run -d --name miweb -p 8081:80 \
                            -v $WORKSPACE:/usr/share/nginx/html \
                            nginx:alpine
                        '''
                    }
                }
            }
        }
    }
}
