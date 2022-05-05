---

typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: File Upload
---



# File Upload



En la siguiente práctica vamos a realizar un *reverse shell*  mediante la subida de un archivo ejecutable para que el ordenador de la  víctima se conecte al ordenador del atacante al visitar una url.

## Paso 1

Vamos a *subir* un archivo `php` que contiene el código del *reverse shell* mediante la opción de menú *File Upload*.



## Paso 2

Descarga el archivo del *reverse shell* desde esta [dirección](https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php) y guárdalo como `shell.php`

## Paso 3

Edítalo y cambia la IP por la de tu equipo

## Paso 4

Ahora sube el archivo mediante el menú `Upload`, fijándote en la url que genera.

## Paso 5

Ya sólo nos queda ejecutar en el ordenador del atacante el comando `netcat`

```
1   nc -v -n -l -p 1234 
```



![resultado_fileupload](/assets/img/resultado_fileupload.png)

