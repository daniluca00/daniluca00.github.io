---

typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Dependency Track
---





# Dependency Track

Dependency Track es un proyecto de la OWASP que permite una gestión de las dependencias y de sus vulnerabilidades.

Dependency-Track monitorea el uso de componentes en todas las versiones  de cada aplicación en su cartera para identificar proactivamente el  riesgo en una organización. La plataforma tiene un diseño basado en API y es ideal para su uso en entornos de CI/CD.



### Instalación

```

curl -LO https://dependencytrack.org/docker-compose.yml

docker-compose up -d 

```



![dependency1](/assets/img/dependency1.png)



Una vez montado accederemos a nuestro "localhost" por el puerto 8080 



![dependency2](/assets/img/dependency2.png)



Nos creamos un  Proyecto Nuevo y indicamo s Upload BOM y le ponemos el ```bom.xml``` descargado. Nuestro proyecto será protonmail.webclient.

![dependency3](/assets/img/dependency3.png)



Por ultimo podremos ver las vulnerabilidades de los componentes de la aplicación.



![dependency5](/assets/img/dependency5.png)

