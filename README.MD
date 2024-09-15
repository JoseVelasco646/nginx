# Proxy Reverse 
Este documento es para configurar un Dodcker con Nginx con el puerto 80, instalar dentro de ese docker Python.

1. [Descargar docker](#Descargar)

2. [Descargar el Docker de nginx](#Desccargar-Docker-de-nginx)

3. [Configurar nginx](#Configurar-nginx)

4. [Instalar paquetes](#Instalacion-de-paquetes)
5. [Creacion de usuario](#Crear-de-usuario)
6. [Crear proxy reverse](#Proxy)

## Descargar
Lo primero que tenemos que hacer es instalar Docker.
https://www.docker.com/.  
Nos dirigimos al link para instalar docker, para poder instalarlo por favor de leer la documentacion para no tener problemas al descargarlo.

## Desccargar-Docker-de-nginx
Para Instalar el contenedor nos vamos a https://hub.docker.com/, aqui buscamos el contenedor de nginx.  
Para Descargarlo nos vamos a la terminal y ponemos el siguiente comando `docker pull nginx`.  

## Configurar-nginx
Para configurar nginx, primero verificamos que la imgen este descargar con el siguiente comando `docker image ls`, como usaremos linux, tendremos que poner `sudo` antes de cualquier codigo.  
Ahora creamos el contenedor de ngix con el siguiente comando `sudo docker run --name nginxx -p 80:80 -d nginx` con este comando creamos un nuevo contenedor, ahora verifcamos que se ha creado el contenedor con el comando `sudo docker ps`, nos deberia de mostrar el contenedor ejecutandose.

## Instalacion-de-paquetes
Una vez que tengamos ejecutando el contenedor de nginx entramos a el, con el comando `sudo docker exec -it nginxx bash`. Dentro del contenedor tendremos que descargar python3, el entorno virtual de python, vim, etc.  
Para instalar python3 primero actualizamos los paquetes con el comando `apt update`, ahora instalamos python3, `apt install python3`, instalamos el entorno virtual `apt install python3`, y por ultimo instalmos vim `apt install vim`.  

## Creacion-de-usuario
Una vez que tengamos instlado lo anterior procedemos a crear un usario con el comando `adduser "name"` y le agregamos los datos que nos pide, ahora para acceder al usuario solo usamos el comando `su "name"`, para salir del usuario solo usamos el comando `exit`

## Proxy
Para crear un proxy reverse nos iremos primero a la carpeta de home y dentro estar un archivo con el nombre de nuestro usuario, lo primero que tendremos que hacer es crear un entorno virutal con el siguiente comando `apython3 -m venv nombre_del_entorno`, accedemos a la carpeta con el comando `cd nombre de la carpeta` aqui creamos un archivo de python, para eso usamos el siguiente comando `vim hello.py` dentro del archivo escrimos el ejemplo de flask, entramos al siguiete link https://flask.palletsprojects.com/en/3.0.x/quickstart/  aqui encontraremos el ejemplo de flask y lo copiamos y ponemos en el archivo que creamos para poder escribir presionamos la letra `i`. Ahora guardamos y salimos del archivo, para guardar presionamos la letra `Esc` ahora preionamos `shift + :` y escribimos `wq` con esto se guardara el archivo y saldremos del editor de vim.  
Y por ultimo viene la configuracion del proxy reverse, pero antes de eso tendremos que activar el entorno virtual e instalar la libreria de Flask, si no no funciona, para activar el entorno virtual usamos el comando `source bin/activate` ahora procedemos instalar Flask con el comando `pip install Flask` y procedemos a ejecutar flask con el siguiente comando `flask --app hello run` esto lo ponemos en la terminal y flask se deberia de estar ejecutandose en el puerto 5000, ahora configuramos el proxy reverse, para esto nos iremos al directorio principal, llegaremos usando `cd` una vez ahi saldremos del usuario para poder modifcar el archivo de default.conf de nginx y no tener problemas, salimos con `exit` ahora iremos a la carpeta de `etc/nginx/conf.d/` y editamos el archivo `default.conf` nos vamos a la linea 21 y agregamos el siguiente comando `location /pagina{`  
        `proxy_pass http://127.0.0.1:5000;`  
        `proxy_set_header Host "localhost";}`  
ahora guardamos y salimos del archivo. (`wq`) lo que queda es reiniciar nginx con el comando `nginx -s reload` y ya tendriamos el proxy reverse, ahora solo ejecutamos de nuevo el ejemplo de flask y probamos en el navegador `localhost/pagina`.  
Cualquier duda se la guardan.