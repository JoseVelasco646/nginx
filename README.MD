# Proxy Reverse 
Este documento es para configurar un Dodcker con Nginx con el puerto 80, instalar dentro de ese docker Python.

1. [Descargar docker](#Descargar)

2. [Descargar el Docker de nginx](#Desccargar-Docker-de-nginx)

3. [Configurar nginx](#Configurar-nginx)
4. Instalar python3, entorno virtual, vim etc.
5. Crear usuario dentro de docker.
6. Hacer el proxy reverse.

## Descargar
Lo primero que tenemos que hacer es instalar Docker.
https://www.docker.com/.  
Nos dirigimos al link para instalar docker, para poder instalarlo por favor de leer la documentacion para no tener problemas al descargarlo.

## Desccargar-Docker-de-nginx
Para Instalar el contenedor nos vamos a https://hub.docker.com/, aqui buscamos el contenedor de nginx.  
Para Descargarlo nos vamos a la terminal y ponemos el siguiente comando `docker pull nginx`.  

## Congigurar-nginx
Para configurar nginx, primero verificamos que la imgen este descargar con el siguiente comando `docker image ls`, como usaremos linux, tendremos que poner `sudo` antes de cualquier codigo.
