---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Seguridad en Docker

---



##  Escaneo pasivo de vulnerabilidades



### Práctica 1

Descargar https://github.com/christophetd/log4shell-vulnerable-app que contiene, entre otras, la vulnerabilidad [log4shell](https://www.cvedetails.com/cve/CVE-2022-23307/). Generar la imagen y luego escanéala con trivy

![trivy1](/assets/img/trivy1.png)

### Práctica 2 

Realizar un testeo de una imagen de Wordpress (no uses tags recientes, pues no tendrán tantas vulnerabilidades)

![trivy2_wordpress](/assets/img/trivy2_wordpress.png)



### Practica 3

Realizar un testeo con DependencyTrack a partir del BOM generado con [Syft](https://github.com/anchore/syft/), tener en cuenta que el formato de salida debe ser `cyclonedx`.



