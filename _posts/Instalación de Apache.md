## Instalación de Apache 



Primero necesitaremos instalar el servidor web Apache

```
sudo apt-get update

sudo apt-get install apache2

sudo apt-get install php libapache2-mod-php

sudo apt-get install php-mysql
```

Para verificar que esta corriendo tenemos que mirar en localhost o http://127.0.0.1



## Hosts virtuales

Creamos en la ruta de */var/www/html* y creamos nuestra carpeta **dominio1** y creamos un fichero de texto llamado "index.php". (El contenido del fichero debería ser algo así)

>```<?php
><?php
>
>EL contenido de nuestra página.
>
>?>
>```
>
>
>
>



![hosts](/home/dluca/Imágenes/hosts.png)

Una vez creada la carpeta iremos a */etc/hosts* y añadiremos como se llamará nuestra URL del host y con la IP del **localhost**.



Después de realizar la configuración del fichero **/etc/hosts** tendremos que acceder a la configuración del apache2.



Para ello iremos a:  



![available](/home/dluca/Imágenes/available.png)



Una vez aquí tendremos que copiar el fichero *000-default.conf*  y solamente le cambiaremos el nombre y cambiaremos dos cosas.

![000-def](/home/dluca/Imágenes/000-def.png)

Donde está el "*" pondremos el nombre que hemos puesto en el fichero **hosts** en nuestro caso dominio1.local.

Una vez hecho esto guardamos nuestro fichero. Pero no habrémos acabado nos faltarás unos pequeñps pasos.



Tendremos que habilitar nuestro host :

```sudo 
sudo a2ensite dominio1 
```

Con este comando activaremos nuestro host y luego desactivaremos el pordefecto que es el 000-default.conf

```sudo
sudo a2dissite 000-default.conf
```

Por ultimo para que nuestra configuración se aplique sin tener que reiniciar el servicio del servidor web ya que eso no es muy bueno para la imagen de una página web utilizaremos el siguiente comando.

```sudo
sudo systemctl reload apache2
```

