# Proyecto CI/CD con Jenkins y Docker

Este proyecto es la actividad independiente para configurar un flujo de integración y despliegue continuo (CI/CD) usando **Jenkins + Docker**.  
Al final se despliega una página web sencilla (`index.html`) en un contenedor Nginx accesible desde el navegador.

---

## 🚀 Pasos para ejecutar el proyecto

### 1. Clonar el repositorio
```bash
git clone https://github.com/Esteban-Developer/proyecto-jenkins.git
cd proyecto-jenkins
2. Levantar Jenkins y Docker-in-Docker (DinD)
El proyecto incluye un archivo docker-compose.yml que levanta dos servicios:

jenkins → servidor Jenkins LTS (última versión con JDK21).

dind → contenedor Docker-in-Docker que permite a Jenkins ejecutar contenedores.

Ejecuta:

bash
Copiar código
docker compose up -d
3. Configurar Jenkins
Obtener la clave inicial:

bash
Copiar código
docker exec -it jenkins-ci cat /var/jenkins_home/secrets/initialAdminPassword
Abrir http://localhost:8080 en el navegador.

Pegar la clave inicial y completar la instalación.

Instalar los plugins recomendados (incluye Git y Docker Pipeline).

Crear un usuario admin.

4. Crear un Pipeline
En Jenkins, ir a Nuevo Item → Pipeline.

Seleccionar Pipeline script from SCM.

SCM: Git.

URL del repo:

bash
Copiar código
https://github.com/Esteban-Developer/proyecto-jenkins.git
Branch: main.

Guardar.

5. Ejecutar el Pipeline
Cuando corra el pipeline, se realizan los siguientes pasos:

Clonar el código desde GitHub.

Verificar archivos (ls -l y mostrar index.html).

Desplegar un contenedor Nginx sirviendo el archivo index.html.

6. Ver la página desplegada
Abrir en el navegador:

arduino
Copiar código
http://localhost:8081
Deberías ver el mensaje de bienvenida del index.html.

📂 Archivos del proyecto
docker-compose.yml → define los servicios de Jenkins y Docker-in-Docker.

Jenkinsfile → define el pipeline de Jenkins.

index.html → página web de prueba a desplegar.

README.md → instrucciones paso a paso.