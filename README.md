Proyecto CI/CD con Jenkins y Docker

Este proyecto implementa un flujo de integración y despliegue continuo (CI/CD) usando Jenkins + Docker.
El resultado final es el despliegue de una página web sencilla (index.html) en un contenedor Nginx, accesible desde el navegador.

🚀 Pasos para ejecutar el proyecto
1. Clonar el repositorio
git clone https://github.com/Esteban-Developer/proyecto-jenkins.git
cd proyecto-jenkins

2. Levantar Jenkins y Docker-in-Docker (DinD)

El proyecto incluye un archivo docker-compose.yml que levanta dos servicios:

jenkins → Servidor Jenkins LTS (última versión con JDK21).

dind → Contenedor Docker-in-Docker que permite a Jenkins ejecutar contenedores.

Ejecuta:

docker compose up -d

3. Configurar Jenkins

Obtener la clave inicial:

docker exec -it jenkins-ci cat /var/jenkins_home/secrets/initialAdminPassword


Abrir en el navegador 👉 http://localhost:8080
.

Pegar la clave inicial y completar la instalación.

Instalar los plugins recomendados (incluye Git y Docker Pipeline).

Crear un usuario admin.

4. Crear un Pipeline

En Jenkins:

Ir a Nuevo Item → Pipeline.

Seleccionar Pipeline script from SCM.

SCM: Git.

URL del repo:

https://github.com/Esteban-Developer/proyecto-jenkins.git


Branch: main.

Guardar.

5. Ejecutar el Pipeline

Cuando corras el pipeline, Jenkins hará lo siguiente:

Clonar el código desde GitHub.

Verificar los archivos (ls -l y mostrar contenido de index.html).

Eliminar cualquier contenedor previo llamado miweb.

Desplegar un nuevo contenedor Nginx, montando la carpeta de trabajo de Jenkins (/var/jenkins_home/workspace/proyecto-jenkins) en /usr/share/nginx/html.

De esta manera, cada vez que actualices el index.html en GitHub y ejecutes el pipeline, el cambio se verá reflejado automáticamente en el navegador.

6. Ver la página desplegada

Abrir en el navegador:

http://localhost:8081


Deberías ver el contenido de tu index.html personalizado. ✅

📂 Archivos del proyecto

docker-compose.yml → Define los servicios de Jenkins y Docker-in-Docker.

Jenkinsfile → Define el pipeline de Jenkins.

index.html → Página web de prueba a desplegar.

README.md → Instrucciones paso a paso.
