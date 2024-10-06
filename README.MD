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
