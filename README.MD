# Proxy Reverse

Este documento describe cómo configurar un contenedor Docker con Nginx en el puerto 80 e instalar Python dentro de dicho contenedor.

## Tabla de Contenidos

1. [Descargar Docker](#Descargar-docker)
2. [Descargar contenedor de Nginx](#Descargar-contenedor-Nginx)
3. [Configurar Nginx](#configurar-Nginx)
4. [Instalación de paquetes](#Instalación-de-paquetes)
5. [Creación de usuario](#Creación-de-usuario)
6. [Crear Proxy Reverse](#crear-proxy-reverse)

## Descargar Docker

Lo primero que debemos hacer es instalar Docker. Dirígete a [Docker](https://www.docker.com/) para descargarlo. Asegúrate de leer la documentación para evitar problemas durante la instalación.

## Descargar contenedor de Nginx
Para instalar el contenedor de Nginx, visita [Docker Hub](https://hub.docker.com/) y busca el contenedor de Nginx. Luego, en la terminal, ejecuta el siguiente comando:
```bash
docker pull nginx
```
Para configurar Nginx, primero verifica que la imagen se haya descargado con el siguiente comando:
```bash
sudo docker image ls
```
Ahora, crea el contenedor de Nginx con el siguiente comando:
```bash
sudo docker run --name nginxx -p 80:80 -d nginx
```

Verifica que el contenedor esté ejecutándose:
```bash
sudo docker ps
```

## Instalación de paquetes
Una vez que tengas el contenedor de Nginx en ejecución, accede a él con el comando:

```bash
sudo docker exec -it nginxx bash
```
Dentro del contenedor, actualiza los paquetes e instala Python 3 y otros utilitarios necesarios:
```bash
apt update
apt install python3
apt install python3-venv
apt install vim

```
## Creación de usuario
```bash
adduser "nombre_de_usuario"
```

Sigue las instrucciones que aparecen en pantalla. Para acceder al nuevo usuario, utiliza:
```bash
su "nombre_de_usuario"
```
Para salir del usuario, simplemente usa el comando:
```bash
exit

```

## Crear Ejemplode Flask
Para crear un proxy reverse, dirígete primero a la carpeta de inicio del usuario y crea un entorno virtual:
```bash
python3 -m venv nombre_del_entorno
cd nombre_de_carpeta
```
Crea un archivo de Python:
```bash
vim hello.py
```
Dentro de este archivo, escribe el ejemplo de Flask que puedes encontrar en la [documentación de Flask](https://flask.palletsprojects.com/en/1.1.x/quickstart/).
* En la linea 4 donde viene `@app.route("/")` cambiarlo a `@app.route("/pagina")`
* Presiona `i` para entrar en modo de inserción.
* Después de escribir el código, presiona Esc, luego `Shift + :` , y finalmente escribe `wq` para guardar y salir.

Descargar Flask
```bash
pip install Flask
```

Ahora, activa el entorno virtual e instala Flask:
```bash

source bin/activate
pip install Flask
```
Ejecuta Flask con el siguiente comando:
```bash
flask --app hello run
```
Flask debería estar ejecutándose en el puerto 5000.

## Crear Proxy Reverse
Dirígete al directorio principal del contenedor. Usa `cd` para navegar y sal del usuario actual con `exit`.  
Ahora ve a la carpeta de configuración de Nginx:
```bash
cd /etc/nginx/conf.d/
```
Edita el archivo default.conf. Ve a la línea 21 y añade la siguiente configuración:
```bash
location /pagina {
    proxy_pass http://127.0.0.1:5000;
    proxy_set_header Host "localhost";
}
```
Guarda y sal del archivo `wq`.  
Reinicia Nginx con el siguiente comando:
```bash
nginx -s reload
```
Ahora, ejecuta de nuevo el ejemplo de Flask y prueba en el navegador accediendo a `http://localhost/pagina`.
