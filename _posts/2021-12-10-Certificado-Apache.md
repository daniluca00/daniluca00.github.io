---

typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Instalación de un certificado digital en Apache
---

# Instalación de un certificado digital en Apache2



## Paso 1

Para empezar necesitaremos tener el module de apache2 del ssl activado. Para esto necesitaremos habilitarlo y luego reiniciar el servicio de apache2



```bash
sudo a2enmod ssl
sudo service apache2 restart
```




## Paso 2

Luego crearemos una carpeta en la la carpeta de configuración de apache donde crearemos nuestro certificado autofirmado.
```bash
sudo mkdir /etc/apache2/ssl

```


```bash
sudo openssl req -x509 -nodes -days 365 \ 
-newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt
```







## Paso 3

Una vez creadas el certificado y la clave tendremos que modificar el fichero de configuración del ssl en este caso */etc/apache2/sites-available/default-ssl.conf*

Modificaremos este fichero con nuestras rutas 



![default_ssl](/ciber/Documentos/Repos/daniluca00.github.io/assets/img/default_ssl.png)







## Paso 4

Modificaremos el fichero /etc/hosts para añadir la URL del ssl.



![hosts_ssl](/ciber/Documentos/Repos/daniluca00.github.io/assets/img/hosts_ssl.png)



## Paso 5

Habilitamos el archivo default-ssl.conf y reiniciamos el servicio.

```bash
sudo a2ensite default-ssl.conf
sudo systemctl restart apache2
```



## Paso 6

Ponemos la URL https://www.midominioseguro.com y nos sacará el certificado. 



![www.midominioseguro](/home/ciber/Documentos/Repos/daniluca00.github.io/assets/img/www.midominioseguro.png)



