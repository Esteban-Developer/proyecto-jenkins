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
                          # Eliminar contenedor viejo si existe
                          docker rm -f miweb || true
                          
                          # Crear nuevo contenedor Nginx, montando TODA la carpeta
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
