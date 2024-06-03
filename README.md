# Creación y compilación de Docker Image de Nagios Core

Este conjunto de instrucciones te guiará a través del proceso de creación y compilación de una imagen Docker de Nagios Core, lo que te permitirá implementar un sistema de monitoreo de red eficiente.

## Introducción

La creación de una imagen Docker de Nagios Core facilita la implementación y administración de un sistema de monitoreo de red altamente efectivo. Esta guía te proporcionará los pasos necesarios para llevar a cabo este proceso de manera exitosa.

## 1. Preparación del entorno

Antes de comenzar, asegúrate de tener una instancia EC2 de Amazon Linux con acceso SSH y permisos de administrador. Además, verifica que tengas una conexión a Internet desde la instancia EC2. (en caso de hacerlo en AWS)

Crea un directorio donde se copiarán los archivos necesarios:

mkdir /opt/nagios-core-docker
cd /opt/nagios-core-docker/

Descarga los archivos necesarios:

wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.9.tar.gz
tar xzf nagios-4.4.9.tar.gz

wget https://github.com/nagios-plugins/nagios-plugins/releases/download/release-2.4.2/nagios-plugins-2.4.2.tar.gz
tar xzf nagios-plugins-2.4.2.tar.gz

wget https://github.com/NagiosEnterprises/nrpe/releases/download/nrpe-4.1.0/nrpe-4.1.0.tar.gz
tar xzf nrpe-4.1.0.tar.gz

**Verificación de integridad de archivos descargados:** Se recomienda verificar la integridad de los archivos descargados mediante la comprobación de su suma de comprobación (checksum).

## 2. Configuración de las credenciales de autenticación

Define las credenciales de autenticación básicas de Nagios en el archivo `.env`. Puedes modificar este archivo según las credenciales de autenticación que necesites utilizar.

NAGIOSADMIN_USER=nagiosadmin
NAGIOSADMIN_PASSWORD=password

## 3. Compilación de la imagen Docker

Construye la imagen Docker utilizando el Dockerfile proporcionado.

docker build -t nagios-core:4.4.9 .

## 4. Ejecución del contenedor Docker

Crea y ejecuta el contenedor de Nagios-Core utilizando el siguiente comando:

docker run --name nagios-core-4.4.9 -dp 80:80 nagios-core:4.4.9

Si necesitas anular las credenciales definidas en el archivo `.env`, usa el siguiente comando:

docker run -e NAGIOSADMIN_USER_OVERRIDE=monadmin -e NAGIOSADMIN_PASSWORD_OVERRIDE=password --name nagios-core-4.4.9 -dp 80:80 nagios-core:4.4.9

## 5. Acceso a la interfaz web principal de Nagios

Verifica si todo está bien accediendo a la interfaz web de Nagios Core en:

http://docker-host-IP-or-hostname/nagios/

**Seguridad y mejores prácticas:** Recuerda configurar contraseñas seguras, limitar el acceso a la interfaz web y configurar cortafuegos para restringir el acceso no autorizado.

**Automatización del proceso de construcción:** Si es relevante para tu caso de uso, considera automatizar el proceso de construcción de la imagen Docker utilizando herramientas como Docker Compose o Terraform.

**Personalización de la configuración de Nagios Core:** Explora cómo personalizar la configuración de Nagios Core según tus necesidades específicas, como agregar hosts, servicios, contactos y notificaciones.

**Recursos adicionales:** Consulta la documentación oficial de Nagios Core, tutoriales en línea y foros de la comunidad para obtener más información sobre Nagios Core y Docker.
