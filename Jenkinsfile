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
                          # Borrar cualquier contenedor viejo
                          docker rm -f miweb || true
                          
                          # Crear contenedor nuevo y montar el workspace completo
                          docker run -d --name miweb -p 8081:80 \
                            -v /var/jenkins_home/workspace/proyecto-jenkins:/usr/share/nginx/html \
                            nginx:alpine
                        '''
                    }
                }
            }
        }
    }
}
