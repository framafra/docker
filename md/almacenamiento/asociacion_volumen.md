## Volúmenes docker

Si elegimos conseguir la persistencia de datos usando volúmenes estamos haciendo que los datos de los contenedores que nosotros decidamos se almacenen en una parte del sistema de ficheros que es gestionada por docker y a la que, debido a sus permisos, sólo docker tendrá acceso. En linux se guardan en `/var/lib/docker/volumes`. Este tipo de volúmenes se suele usar en los siguiente casos:

* Para compartir datos entre contenedores. Simplemente tendrán que usar el mismo volumen.
* Para copias de seguridad ya sea para que sean usadas posteriormente por otros contenedores o para mover esos volúmenes a otros hosts.
* Cuando quiero almacenar los datos de mi contenedor no localmente si no en un proveedor cloud.

### Gestionando volúmenes

Los volúmenes se pueden crear sin necesidad de asociarlo a un contenenos. Esto lo podemos hacer con el comando `docker volume`.  
Algunos comando útiles para trabajar con volúmenes docker:

* `docker volumen create mivolumen`: Crea un volumen con el nombre "mivolumnen" vacío.
* `docker volume rm mivolumen`: Elimina el volumen "mivolumen", siempre que todo contenedor que lo utilice esté parado.
* `docker volumen prune`: Para eliminar los volúmenes que no están siendo usados por ningún contenedor.
* `docker volume ls`: Nos proporciona una lista de los volúmenes creados y algo de información adicional.
* `docker volume inspect`: Nos dará una información mucho más detallada de el volumen que hayamos elegido.


Una vez creado el volumen lo podemos asociar a cualquier contenedor con el flag `--volume` o `-v`.

!!! Note "Si usamos imágenes de DockerHub, debemos leer la información que cada imagen nos proporciona en su página ya que esa información suele indicar cómo persistir los datos de esa imagen, ya sea con volúmenes o bind mounts, y cuáles son las carpetas importantes en caso de ser imágenes que contengan ciertos servicios (web, base de datos etc...)"

## Ejemplo usando volúmenes docker

Lo primero que vamos a hacer es crear un volumen docker:

```bash
$ docker volume create mivol
mivol
```

A continuación creamos un contenedor con el volumen asociado, usando `--mount`, y creamos un fichero `index.html`:

```bash
$ docker run -d --name apa -v mivol:/usr/local/apache2/htdocs -p 81:80 httpd:2.4
b51f89eb21701362279489c5b52a06b1a44c10194c00291de895b404ab347b80

$ docker exec apa bash -c 'echo "<h1>Volumen de prueba</h1>" > /usr/local/apache2/htdocs/index.html'
```

Accedemos a un navegador y probamos la web http://localhost:81

Borramos el contenedor.

```
$ docker rm -f apa
apa
```

Después de borrar el contenedor, volvemos a crear otro contenedor con el mismo volumen asociado:

```bash
$ docker run -d --name apa1 -v mivol:/usr/local/apache2/htdocs -p 82:80 httpd:2.4
baa3511ca2227e30d90fa2b4b225e209889be4badff583ce58ac1feaa73d5d77
```

Y podemos comprobar en un navegador web http://localhost:82 que no se ha perdido la información (el fichero `index.html`):


Algunas aclaraciones:

* Al no indicar el volumen, se creará un nuevo volumen.
* Si usamos el flag `-v` e indicamos un nombre, se creará un volumen docker nuevo.
* Al usar tanto volúmenes como bind mount, el contenido de lo que tenemos sobreescribirá la carpeta destino en el sistema de ficheros del contenedor en caso de que exista.



Para más información sobre volumenes puedes consultar [https://docs.docker.com/storage/volumes/](https://docs.docker.com/storage/volumes/)