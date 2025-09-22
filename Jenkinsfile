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
                          # Eliminar si existe contenedor viejo
                          docker rm -f miweb || true
                          
                          # Crear nuevo contenedor Nginx limpio
                          docker run -d --name miweb -p 8081:80 nginx:alpine
                          
                          # Sobrescribir el index.html por el nuestro
                          docker cp /var/jenkins_home/workspace/proyecto-jenkins/index.html miweb:/usr/share/nginx/html/index.html
                        '''
                    }
                }
            }
        }
    }
}
