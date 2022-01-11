---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories: 
conToc: true
title: WordPress
---



## Wordpress

Vamos a instalar Wordpress en un contenedor.

1.- Creamos un directorio vacío  donde estará situado nuestro Wordpress.

```bash
mkdir my_wordpress
```

2.- Dentro del directorio deberemos tener un fichero " *docker-compose.yml* ". Dentro de dicho archivo tendremos unas instrucciones que iniciarán nuestro blog de Wordpress y una instancia de MySQL separada con un montaje de volumen para persistencia de datos:



```bash
version: '3.3'

services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
volumes:
    db_data: {}
```



Una vez tengamos montado nuestro proyecto tendremos ejecutar en el directorio :

![docker-compose up -d](/home/ciber/Documentos/Repos/daniluca00.github.io/assets/img/docker-compose up -d.png)

Este comando ```docker-compose up -d``` lo que hace es extraer las Imagenes de Docker necesarias e inicia los contenedores de Wordpress.

Por ultimo para comprobar el funcionamiento iremos a http://localhost:8000 y nos abrirá nuestro docker de Wordpress.

![wordpress_instalación](/home/ciber/Documentos/Repos/daniluca00.github.io/assets/img/wordpress_instalación.png)