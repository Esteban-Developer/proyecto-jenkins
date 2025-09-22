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
                          echo "🔹 Eliminando contenedor anterior si existe..."
                          docker rm -f miweb || true
                          
                          echo "🔹 Creando nuevo contenedor Nginx..."
                          docker run -d --name miweb -p 8081:80 nginx:alpine
                          
                          echo "🔹 Copiando index.html al contenedor..."
                          docker cp /var/jenkins_home/workspace/proyecto-jenkins/index.html miweb:/usr/share/nginx/html/index.html
                          
                          echo "✅ Despliegue completado. Accede a http://localhost:8081"
                        '''
                    }
                }
            }
        }
    }
}
