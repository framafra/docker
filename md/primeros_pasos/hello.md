# El "Hola Mundo" de docker

Vamos a comprobar que todo funciona creando nuestro primer contenedor desde la imagen `hello-world`:

```bash
$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete 
Digest:     sha256:31b9c7d48790f0d8c50ab433d9c3b7e17666d6993084c002c2ff1ca09b96391d
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working     correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs    the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which  sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

Pero, ¿qué es lo que está sucediendo al ejecutar esa orden?:

* Si nos fijamos en el comienzo de la información mostrada, concretamente en la
primera fila (_Unable to find image 'hello-world:latest' locally_), ahí se nos indica que la imagen hello-word:latest no está localmente en nuestro
sistema. Al no estar, la imagen `hello-word` se descarga desde el repositorio que se encuentra en el registro que vayamos a utilizar, en nuestro caso DockerHub. De hecho, si volvemos a hacer el comando “docker run hello-world”, al tener la imagen ya en el sistema, no nos aparecerá este texto, ya que la imagen la tenemos almacenada localmente.
* Otro aspecto a destacar, es que pese a que solo hemos escrito hello-world, nos ha descargado una imagen llamada hello-world:latest. Esto es porque cada imagen creada tiene un nombre de versión. Si no indicamos nada o indicamos latest, nos instala la última versión. Si queremos instalar una versión concreta de una imagen se indica de la forma imagen:nombreversion.
* Y  por último podemos observar que muestra el mensaje de bienvenida que es la consecuencia de ejecutar un comando al crear y arrancar un contenedor basado en esa imagen.

Si listamos los contenedores que se están ejecutando (`docker ps`):

```bash
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```
Comprobamos que este contenedor no se está ejecutando. **Un contenedor ejecuta un proceso y cuando termina la ejecución, el contenedor se para.**

Para ver los contenedores que no se están ejecutando:

```bash
$ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
372ca4634d53        hello-world         "/hello"            8 minutes ago       Exited (0) 8 minutes ago                       elastic_johnson
```

Para eliminar el contenedor podemos identificarlo con su `id`:

```bash
$ docker rm 372ca4634d53
```

o con su nombre:

```bash
$ docker rm elastic_johnson
```
<br>

!!! note "Buscar imagenes"
      * Para buscar las imágenes de cualquier sistema, utilizaremos la orden:
      
            $docker search NombreImagen
      
      El script rastreará Docker Hub y nos ofrecerá una lista de todas las imágenes que tengan un nombre que concuerde con la búsqueda lanzada.
      
!!! note "Descargar imagenes"
     * Para descargar la imagen que queremos, utilizaremos la orden:
  
         $docker pull NombreImagen

      Después de descargar una imagen, se puede ejecutar un contenedor utilizando la imagen descargada con el comando run. Si no se ha descargado la imagen previamente, automáticamente Docker primero descargará la imagen y después ejecutará un contenedor con la imagen descargada.

!!! note "Ver las imagenes descargadas"
      * Para ver las imágenes que tenemos descargadas, utilizaremos la orden:
      
         $docker images
