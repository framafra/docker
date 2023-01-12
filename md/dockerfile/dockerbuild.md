El comando `docker build` construye la nueva imagen leyendo las instrucciones del fichero `Dockerfile` y la información de un **entorno**, que para nosotros va a ser un directorio (aunque también podemos guardar información, por ejemplo, en un repositorio git).

La creación de la imagen es ejecutada por el *docker engine*, que recibe toda la información del entorno, por lo tanto es recomendable guardar el `Dockerfile` en un directorio vacío y añadir los ficheros necesarios para la creación de la imagen. El comando `docker build` ejecuta las instrucciones de un `Dockerfile` línea por línea y va mostrando los resultados en pantalla.

Tenemos que tener en cuenta que cada instrucción ejecutada crea una imagen intermedia, una vez finalizada la construcción de la imagen nos devuelve su id. Algunas imágenes intermedias se guardan en **caché**, otras se borran. Por lo tanto, si por ejemplo, en un comando ejecutamos `cd /scripts/` y en otra linea le mandamos a ejecutar un script (`./install.sh`) no va a funcionar, ya que ha lanzado otra imagen intermedia. Teniendo esto en cuenta, la manera correcta de hacerlo sería:

```bash
cd /scripts/;./install.sh
```

Para terminar indicar que la creación de imágenes intermedias generadas por la ejecución de cada instrucción del `Dockerfile`, es un mecanismo de caché, es decir, si en algún momento falla la creación de la imagen, al corregir el `Dockerfile` y volver a construir la imagen, los pasos que habían funcionado anteriormente no se repiten ya que tenemos a nuestra disposición las imágenes intermedias, y el proceso continúa por la instrucción que causó el fallo.

## Ejemplo de  Dockerfile

Vamos a crear una imagen con ubuntu, al cuál le vamos a instalar apache y vamos a poner una web (index.html) con nuestro nombre.  
Para ellos creamos un directorio en nuestro pc llamado miprimerdockerfile, en ese directorio colocaremos el fichero `index.html` y crearemos un fichero llamado Dockerfile

El contenido de `Dockerfile` será:

```Dockerfile
FROM ubuntu:latest
MAINTAINER Paco Maño "fj.manofrasquet@edu.gva.es"
RUN apt update  && apt install -y  apache2 
COPY index.html /var/www/html/
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
```

Para crear la imagen uso el comando `docker build`, indicando el nombre de la nueva imagen (opción `-t`) y indicando el directorio contexto.

```bash
$ docker build -t framafra/ubuntuapache:v1 .
```
!!! note "Nota: Ponemos como directorio el `.` porque estamos ejecutando esta instrucción dentro del directorio donde está el `Dockerfile`. A la imagen que voy a crear la llamos framafra/ubuntuapache y le pongo el tag de v1"


Una vez terminado, podríamos ver que hemos generado una nueva imagen:

```bash
$ docker images
REPOSITORY                  TAG                 IMAGE ID            CREATED             SIZE
framafra/ubuntuapache       v1                4816f9eee434        11 seconds ago      225MB
...
```

Ahora podemos crear el contendor a partir de la imagen creada, ejecutando el siguiente comando:

```bash
$ docker run -d -p 8080:80 --name web_server framafra/ubuntuapache:v1 
```            
