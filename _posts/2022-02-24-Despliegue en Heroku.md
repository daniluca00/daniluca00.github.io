---

typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Jenkins Calculator
---





# Despliegue en Heroku

**Heroku** es una plataforma como servicio (PaaS) de computación en la  nube que soporta distintos lenguajes de programación.



## Instalación

Para empezar tendremos que instalar heroku en nuestro sistema.



![heroku1](/assets/img/heroku1.png)



Una vez instalado y hecho el login nos abrirá una  ventana del navegador donde nos pedirá que hagamos el log in 

Podremos implementarle el multifactor de autentificación.

![heroku2](/assets/img/heroku2.png)



## Preparar la aplicación

Lo siquiente que realizaremos sera preparar nuestra Aplicación que utilizaremos de ejemplo para esta practica.

![heroku3](/assets/img/heroku3.png)



Ahora tenemos un repositorio git en funcionamiento que contiene una aplicación simple, un archivo `runtime.txt` que especifica qué versión de Python se usará y un archivo `requirements.txt`, que usa el administrador de dependencias de Python, `Pip`.

## Desplegar la aplicación

Ahora procederemos a desplegar nuestra aplicación. Crearemos una aplicación en Heroku para que reciba nuestro codigo fuente:

![heroku4](/assets/img/heroku4.png)



Cuando creamos una aplicación, también se crea un de `git remote` (llamado `heroku`) y se asocia con su repositorio de git local. Heroku genera un nombre aleatorio (en este caso, `whispering-plains-41029.git`) para la aplicación, o puedes pasar un parámetro para especificar su propio nombre de aplicación.

Una vez creada la aplicación en heroku deberemos desplegar nuestro código:

![heroku5](/assets/img/heroku5.png)

Una vez esto podremos abrir nuestra aplicación mediante ```heroku open```.



## Escalar la aplicación

En Heroku existen los "dynos" que es como un contenedor ligero y estos son gratiutos.

Podremos verificar cuantos "dynos" tenemos mediante el siguiente comando.

![heroku6](/assets/img/heroku6.png)

De forma predeterminada, la aplicación se implementa en un dyno  gratuito. Los dynos gratuitos dormirán después de media hora de  inactividad (si no reciben tráfico). Esto provoca un retraso de unos  segundos para la primera solicitud al despertar. Las solicitudes  posteriores se realizarán con normalidad. Los dynos gratuitos también  consumen de una cuota mensual a nivel de cuenta de horas de dyno  gratuitas; siempre que la cuota no se agote, todas las aplicaciones  gratuitas pueden continuar ejecutándose.

Para escalar una aplicación en Heroku será cambiar el numero de "dynos" de una aplicación: Por ejemplo, podemos escalar el número de dynos web a cero:

```
heroku ps:scale web=0 
```

Lo que producirá un error al refrescar la web porque no tenemos ningún dyno disponible.

Vamos a escalarlo de nuevo:

```
heroku ps:scale web=1 
```



## Instalar las dependencias de la aplicación localmente

Para instalar las dependencias localmente, primero queremos crear un  “Entorno virtual” (también conocido como “venv”) en el que podamos  instalar los paquetes sin afectar la instalación de Python en su  sistema. Para hacer esto, instalamos el entorno virtual de python  mediante `sudo apt install python3.8-venv`  y posteriormente creamos un nuevo entorno virtual:

```
python3 -m venv venv
```

Luego lo activamos:

```
source venv/bin/activate 
```

Ahora ya podemos instalar las dependencias con el ``pip`` 

```
pip install -r requirements.txt
```



![heroku7](/assets/img/heroku7.png)

## Ejecutar la aplicación localmente

La aplicación está casi lista para iniciarse localmente. [Django](https://www.djangoproject.com/) usa activos locales (`assets`), por lo que primero debemos ejecutar `collectstatic`:

![heroku8](/assets/img/heroku8.png)

Una vez ejecutado el comando anterior ejecutaremos ``heroku local`` y ya podremos ver en nuestro localhost nuestra aplicación.

![heroku9](/assets/img/heroku9.png)



![heroku10](/assets/img/heroku10.png)

## Subir cambios locales

Una vez tenemos nuestra aplicación acabada podremos subirla a nuestro repositorio en este caso será en Github.

![heroku11](/assets/img/heroku11.png)

![heroku12](/assets/img/heroku12.png)