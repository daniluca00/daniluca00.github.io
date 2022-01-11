---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories: 
conToc: true
title: Docker HUB
---

# Docker HUB



Que es Docker Hub ? 

Pues Docker Hub es un repositorio publico, por lo que es el lugar perfecto para compartir tus imágenes con el mundo entero. Obviamente, si ese no es el objetivo, exiten otros registros de tipo privado.



## Publicar Imagen



Primero para publicar una imagen necesitaremos una cuenta para eso tendremos que acceder a la web : https://hub.docker.com . Una vez tengamos la cuenta podremos utilizar el terminar y poner :

```bash
docker login
```

Con esto nos loguearemos

Una vez logueados 

```bash
docker tag local-image:tagname new-repo:tagname
```

En nuestro caso lo harémos con nuestra imagen de la practica anterior "chapter2".



![1](/assets/img/1.png)



Con este comango lo que hacemos es como un commit de nuestra imagen.

Luego ejecutamos:

```bash 
docker push new-repo:tagname
```



![2](/assets/img/2.png)

Para comprobar que se ha subido correctamente vamos a la página de Docker Hub y comprobamos que se ha subido.



![3](/assets/img/3.png)