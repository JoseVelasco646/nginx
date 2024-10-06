# Proxy Reverse

Este documento describe cómo configurar un contenedor Docker con Nginx en el puerto 80 e instalar Python dentro de dicho contenedor.

## Tabla de Contenidos

1. [Descargar Docker](#descargar-docker)
2. [Descargar el contenedor de Nginx](#descargar-contenedor-nginx)
3. [Configurar Nginx](#configurar-nginx)
4. [Instalación de paquetes](#instalacion-de-paquetes)
5. [Creación de usuario](#creacion-de-usuario)
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
