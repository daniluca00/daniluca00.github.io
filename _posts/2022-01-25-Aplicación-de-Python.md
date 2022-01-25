---
typora-copy-images-to: ../assets/img
typora-root-url: ../
layout: post
categories: 
conToc: true
title: Aplicación de Python
---





# Aplicación en Python

En este aplicación vamos a trabajar con docker, docker-compose, branches y tags .



Para empezar tenemos que crear un repositorio en GitHub y clonarlo en en nuestro equipo local.



Una vez creado el repositorio tendremos que crear una estructura parecida a esta.

![estructura](/assets/img/estructura.png)







Dentro del Dockerfile tendremos lo siguiente:



```bash
FROM python:3.4
RUN pip install Flask==0.10.1 requests==2.5.1 redis==2.10.3
WORKDIR /app
COPY app /app
CMD ["python", "identidock.py"]
```



Como podemos ver en el Dockerfile instalamos varios dockers en la imagien de nuestro proyecto.



En el *docker-compose.yml* tendremos :

```bash
identidock:
  build: .
  ports:
    - "5000:5000"
  volumes:
    - ./app:/app
  links:
    - dnmonster
    - redis
dnmonster:
  ports:
    - "5080:8080"
  image: amouat/dnmonster:1.0
redis:
  image: redis:3.0
```



Y por ultimo tendremos el codigo en python *identidock.py*  : 

```bash
from flask import Flask, Response, request
import requests
import hashlib
import redis

app = Flask(__name__)
cache = redis.StrictRedis(host = 'redis', port = 6379, db = 0)
salt = "UNIQUE_SALT"
default_name = 'Víctor Ponz'

@app.route('/', methods=['GET', 'POST'])
def mainpage():
	name = default_name
	if request.method == 'POST':
		name = request.form['name']
	salted_name = salt + name
	name_hash = hashlib.sha256(salted_name.encode()).hexdigest()
	header = '<html><head><title>Identidock</title></head><body>'
	body = '''<form method="POST">
			Hola <input type="text" name="name" value="{0}">
			<input type="submit" value="submit">
			</form>
			<p>Te pareces a:
			<img src="/monster/{1}"/>
			'''.format(name, name_hash)
	footer = '</body></html>'
	
	return header + body + footer
@app.route('/monster/<name>')
def get_identicon(name):
	image = cache.get(name)
	if image is None:
		print ("Cache miss", flush=True)
		r = requests.get('http://dnmonster:8080/monster/' + name + '?size=80')
		image = r.content
		cache.set(name, image)
	return Response(image, mimetype='image/png')
		
if __name__ == '__main__':
	app.run(debug=True, host='0.0.0.0')
```



Para poner todo en marcha utilizaremos "docker-compose up -d"

![identickons_2](/assets/img/identickons_2.png)



Si ejecutamos el comando "docker ps " veremos que nos quedará algo asi

![docker_ps](/assets/img/docker_ps.png)



# GitHub entorno de pruebas y producción

Como ya hemos hablado durante el curso la mejor forma de implantar aplicaciones la mejor forma es trabajar primero en un entorno de pruebas donde los tecnicos trabajan para realizar la aplicación. Y luego el entorno de producción donde ya la aplicación definitiva para el cliente. 

Y la forma en la que GitHub nos permite trabajar con eso son con las llamadas "branches" "ramas" en español.

Normalmente la rama "master" es la que se suele utilizar como entorno de producción donde ya esta la aplicacion definitiva. Y luego las branches donde creamos los entornos de pruebas.

```
git branch "nombre" --> creamos una rama nueva
git checkout "nombre" --> cambiamos a la rama
```

Luego  una vez tenemos nuestra aplicación acabada en el entorno de pruebas nos vamos a la rama "master" para ponerla en producción ,para ello :

```
git add * 
git commit -m "Finalizar identicons" 
git checkout master 
```

Ahora procederemos a fusionar las ramas.

```
git merge "nombre" 
```

Luego para eliminar la rama creada para las pruebas.

```
git branch -d "nombre" 
```

Por ultimo como queremos tener siempre constancia de las diferentes versiones de nuestra aplicación creamos "tags".

```
git tag v2.2 
git push origin v2.2 
```



