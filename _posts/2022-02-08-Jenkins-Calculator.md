---

typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories:
conToc: true
title: Jenkins Calculator
---





# Qué es Jenkins

Jenkins es un servidor de automatización de código abierto escrito en  Java. Con un soporte muy activo basado en la comunidad y una gran  cantidad de complementos, es la herramienta más popular para implementar los procesos de Integración Continua y Entrega Continua. Anteriormente  conocido como Hudson, se le cambió el nombre después de que Oracle  comprara Hudson y decidiera desarrollarlo como software propietario.  Jenkins permaneció bajo la licencia del MIT y es muy valorado por su  simplicidad, flexibilidad y versatilidad.



## Instalación de Jenkins con Docker

Primero hay que crear un directorio que luego enlazaremos como un  volumen al correr jenkins. Hemos de cambiar el propietario de dicho  directorio al usado por jenkins (uid 1000) y luego cambiar los permisos

```
mkdir $HOME/jenkins_home 
sudo chown 1000 $HOME/jenkins_home 
sudo chmod 777 $HOME/jenkins_home 
docker run -d -p 49001:8080 -v $HOME/jenkins_home:/var/jenkins_home --name jenkins jenkins/jenkins:lts-jdk11
```



![jenkins2](/assets/img/jenkins2.png)



Visitaremos la url http://localhost:49001/    ( SI entramos por primera vez nos pedirá la contraseña de el administrador, que la podemos recuperar desde ```docker logs jenkins``` o haciendo un ```cat``` del archivo  ```$HOME/jenkins_home/secrets/initialAdminPassword```)



![jenkins_3](/img/jenkins_3.png)

Despues nos pedirá que configuremos un usuario administrador.



![jenkins4](/assets/img/jenkins4.png)



## Jenkins hello world

Todo en todo el mundo de TI comienza con el ejemplo de Hello World.

Sigamos esta regla y veamos los pasos para crear la primera `pipeline` (nombre que se le da a las configuraciones) de Jenkins:

- Haz clic en Nuevo elemento.
- Introduce *hola mundo* como nombre del elemento, elige `Pipeline` y haz clic en **Aceptar**.
- Hay muchas opciones. Las omitiremos por ahora e iremos directamente a la sección Pipeline.
- Allí, en el cuadro de texto Script, podemos ingresar el script de pipeline:

New item



![jenkins5](/assets/img/jenkins5.png)



## Estructura de una pipeline

Una pipeline de Jenkins consta de dos tipos de elementos: **stages** y **steps**. La siguiente figura muestra cómo se utilizan:

Los siguientes son los elementos básicos de la canalización:

- **Step**: una sola operación (le dice a Jenkins qué hacer, por ejemplo, retirar el código del repositorio, ejecutar un script)
- **Stage**: una separación lógica de pasos (agrupa  secuencias de pasos conceptualmente distintas, por ejemplo, compilar,  probar e implementar) que se utiliza para visualizar el progreso de la  canalización de Jenkins.

![jenkins6](/assets/img/jenkins6.png)



Como resultado de esta pipeline obtendremos la siguiente representación visual:



![jenkins7](/assets/img/jenkins7.png)



## Commit pipeline

El proceso de Integración Continua más básico se llama `commit pipeline`. Esta fase clásica, como su nombre lo dice, comienza con un `commit` (o push en Git) al repositorio principal y da como resultado un informe sobre el éxito o el fracaso de la compilación. Ya que se ejecuta  después de cada cambio en el código, la construcción debe tomar no más  de 5 minutos y debe consumir una cantidad razonable cantidad de  recursos. La fase de confirmación es siempre la punto de partida del  proceso de Entrega Continua, y proporciona el ciclo de retroalimentación más importante en el proceso de desarrollo, información constante si el código está en un estado saludable. La fase de compromiso funciona de la siguiente manera. Un desarrollador  comprueba en el código al repositorio, la Integración Continua El  servidor detecta el cambio y se inicia la compilación.

Consta de 3 etapas:

- **Checkout** En esta etapa se descarga el código desde el repositorio
- **Compile** Esta etapa compila el código fuente
- **Test unit** Esta etapa corre una serie de test unitarios

Vamos a crear un proyecto de ejemplo que implemente `commit pipeline`

> Este ejemplo es para un proyecto que usa Git, Java, Gradle y Spring Boot, pero lo mismo aplica para otras tecnologías

### 

### Checkout

En las pipelines la primera acción que debe hacer es hacer un checkout, para ello nos crearemos un nuevo repositorio en github

```
pipeline {
	agent any    
	stages {        
		stage("Checkout") {            
			steps {                
				git url: 'https://github.com/daniluca00/calculator'            
			}        
		}   
	} 
} 
```



La **pipeline** sera ejecutada por cualquier **agente** y su único paso es descargar el código del repositorio. Podemos hacer clic en **Build Now** y comprobar si se ha ejecutado correctamente.



![jenkins8](/assets/img/jenkins8.png)

Pasamos a la segunda fase.

### Compilar

Para compilar un proyecto hemos de:

1. Crear un proyecto con el código fuente
2. Hacer un `push` al repositorio
3. Añadir la etapa `Compilar` a la pipeline

#### Spring Initializr

Vamos a crear un proyecto simple de java usando `gradle` como framework de construcción.

> Spring Boot es un framewrok de Java que simplifica la creación de  aplicaciones empresariales. Gradle es un sistema de automatización de  compilación que se basa en los conceptos de Apache Maven.



> **GIT**
>
> Clonamos el repositorio en local y movemos todos los archivos dentro de la carpeta del mismo con **cuidado** de seleccionar también los archivos **ocultos**



