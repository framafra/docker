En este ejemplo vamos a crear una imágen con una página estática. Vamos a crear tres versiones de la imagen, y puedes encontrar los ficheros en este [directorio](https://github.com/josedom24/curso_docker_2022/tree/main/ejemplos/sesion5/ejemplo1) del repositorio.

## Versión 1: Desde una imagen base

Tenemos un directorio, que en Docker se denomina contexto, donde tenemos el fichero `Dockerfile` y un directorio, llamado `index.html` con nuestra página web:

```bash
$ ls
Dockerfile  index.hmtl
```

En este caso vamos a usar una imagen base de un sistema operativo sin ningún servicio. El fichero `Dockerfile` será el siguiente:

```Dockerfile
FROM debian
RUN apt-get update && apt-get install -y apache2
ADD index.html /var/www/html/
EXPOSE 80
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```

Al usar una imagen base `debian` tenemos que instalar los paquetes necesarios para tener el servidor web, en este acaso apache2. A continuación añadiremos el contenido del directorio `index.hmtl` al directorio `/var/www/html/` del contenedor y finalmente indicamos el comando que se deberá ejecutar al crear un contenedor a partir de esta imagen: iniciamos el servidor web en segundo plano.

Para crear la imagen ejecutamos:

```bash
$ docker build -t framafra/apa:v1 .
```

Comprobamos que la imagen se ha creado:

```bash
$ docker images
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
framafra/apa     v1                  705eb816b4f3        1 minute ago      253MB
```

Y podemos crear un contenedor:

```bash
$ docker run -d -p 81:80 --name webserver1 framafra/apa:v1
```

Y acceder con el navegador a nuestra página:

![ejemplo1](../images/ejemplo1.png){ width="500" }


## Versión 2: Desde una imagen con apache2

En este caso el fichero `Dockerfile` sería el siguiente:

```Dockerfile
FROM httpd:2.4
ADD index.html /usr/local/apache2/htdocs/
EXPOSE 80
```

En este caso no necesitamos instalar nada, ya que la imagen tiene instalado el servidor web. En este caso y siguiendo la documentación de la imagen el *DocumentRoot* es `/usr/local/apache2/htdocs/`. No es necesario indicar el `CMD` ya que por defecto el contenedor creado a partir de esta imagen ejecutará el mismo proceso que la imagen base, es decir, la ejecución del servidor web.

De forma similar, crearíamos una imagen y un contenedor:

```bash
$ docker build -t framafra/apa:v2 .
$ docker run -d -p 82:80 --name webserver2 framafra/apa:v2
```

## Versión 3: Desde una imagen con nginx

En este caso el fichero `Dockerfile` sería:

```Dockerfile
FROM nginx
ADD index.hmtl /usr/share/nginx/html
EXPOSE 80
```

De forma similar, crearíamos una imagen y un contenedor:

```bash
$ docker build -t framafra/ngx:v1 .
$ docker run -d -p 83:80 --name webserver3 framafra/ngx:v1
```
