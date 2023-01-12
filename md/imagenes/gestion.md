Para crear un contenedor es necesario usar una imagen que tengamos descargado en nuestro registro local. Por lo tanto al ejecutar `docker run` se comprueba si tenemos la versión indicada de la imagen y si no es así, se precede a su descarga.

Las principales instrucciones para trabajar con imágenes son:

* `docker images`: Muestra las imágenes que tenemos en el registro local.
* `docker pull`: Nos permite descargar la última versión de la imagen indicada.
* `docker search`: Nos permite buscar imágenes en Docker Hub.
* `docker rmi`: Nos permite eliminar imágenes. No podemos eliminar una imágen si tenemos algún contenedor creada a partir de ella.
* `docker inspect`: nos da información sobre la imágen indicada:
    - El id y el checksum de la imagen.
    - Los puertos abiertos.
    - La arquitectura y el sistema operativo de la imagen.
    - El tamaño de la imagen.
    - Los volúmenes.
    - El ENTRYPOINT que es lo que se ejecuta al hacer `docker run`.
    - Las capas.
    - Y muchas más cosas....
* `docker history`: No permite  ver el historial de una imagen descargada, es decir, en qué versiones se basa.

## Listar imágenes locales
Podemos obtener información de qué imágenes tenemos almacenadas localmente usando:
    
    $docker images

Obteniendo un resultado similar al siguiente:

```bash
$ docker images

REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    a8780b506fa4   4 days ago    77.8MB
httpd        latest    fe8735c23ec5   12 days ago   145MB

```

## Listar imágenes para su descarga
Podemos obtener información de imágenes que podemos descargar en el registro (Docker Hub) utilizando el comando docker search.
Por ejemplo con el siguiente comando:

        $docker search ubuntu

Nos aparecen aquellas imágenes disponibles en Docker Hub con esa palabra.


## Descargar imágenes
Podemos almacenar imágenes localmente desde el registro sin necesidad de crear un contenedor mediante el comando docker pull, claramente inspirado en sistemas de control de versiones como “git”.

    $docker pull ubuntu:20.04

Este comando nos descarga la imagen “ubuntu” con el tag “20.04”, como vemos a continuación:

```
$ docker pull ubuntu:20.04
20.04: Pulling from library/ubuntu
eaead16dc43b: Pull complete
Digest: sha256:450e066588f42ebe1551f3b1a535034b6aa46cd936fe7f2c6b0d72997ec61dbd
Status: Downloaded newer image for ubuntu:20.04
docker.io/library/ubuntu:20.04
```

## Eliminar imágenes con docker rmi
Si queremos eliminar imágenes descargadas que no vamos a utilizar o hemos descargado por error una versión incorrecta, etc., debemos utilizar el comando:

    $docker rmi ubuntu:20.04

!!! Note "Eliminar todas las imágenes que no se están utilizando"
    Una forma de eliminar todas las imágenes locales que no estén siendo utilizadas por un contenedor, es combinando ``docker images -q`` para obtener la lista y ``docker rmi`` para eliminar la lista obtenida.

        $docker rmi $(docker images -q)

## Eliminar todas la imágenes y contenedores
Una forma de realizar las operaciones anteriores de golpe, es usando ``docker system prune -a``, que elimina todas las imágenes y contenedores parados.

- Paso 1. Paramos todos los contenedores (opcional).

        $docker stop $(docker ps -a -q)

- Paso 2. Borramos todos los contenedores.

    $docker system prune -a