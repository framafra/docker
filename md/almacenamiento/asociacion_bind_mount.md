“Binding mount”: básicamente este tipo de persistencia consiste en “montar” un fichero o directorio de la máquina anfitrión en un fichero o directorio del contenedor.  
Este montaje se hace en el momento de crear el contenedor.
- El fichero o directorio se indica en ambos casos con una ruta absoluta no tiene porque existir en el contenedor (si no existe, se creará) .
- El rendimiento de este tipo de persistencia, a efectos prácticos, depende del sistema de ficheros y características hardware de la máquina real. Una buena configuración según las necesidades del contenedor influirá en el rendimiento.
- Estos volúmenes pueden ser usados por varios contenedores simultáneamente.
- En sistemas Linux no suele haber diferencias de rendimiento respecto a volúmenes, pero en sistemas Windows y Mac el rendimiento es peor.


## Ejemplo: montando directorios usando bind mount

En este caso vamos a crear un directorio en el sistema de archivo del host, donde vamos a crear un fichero `index.html`:

```bash
$ mkdir web
$ cd web
/web$ echo "<h1>Montando un bind mount</h1>" > index.html
```

Y podemos montar ese directorio en un contenedor, en este caso usamos la opción `-v`:

```bash
$ docker run -d --name apa -v /home/usuario/web:/usr/local/apache2/htdocs -p 8080:80 httpd:2.4
8de025f6ff4d4b8a5a57d10a9cbb283b103209f358c43148a4716a33a404e208
```

Y comprobamos que realmente estamos sirviendo el fichero que tenemos en el directorio que hemos creado.

```bash
$ curl http://localhost:8080
<h1>Hola</h1>
```

Eliminamos el contenedor y volvemos a crear otro con el directorio montado:

```bash
$ docker rm -f apa
apa

$ docker run -d --name apa1 -v /home/usuario/web:/usr/local/apache2/htdocs -p 8080:80 httpd:2.4
1751b04b0548217d7faa628fd69c10e84c695b0e5cc33b482df2c04a6af83292

$ curl http://localhost:8080
<h1>Hola</h1>
```

Además podemos comprobar que podemos modificar el contenido del fichero aunque este montado en el contenedor:

```bash
$ echo "<h1>Adios</h1>" > web/index.html 
$ curl http://localhost:8080
<h1>Adios</h1>
```

Por último, indicar que si nuestra carpeta origen no existe y hacemos un bind mount con `-v`, esa carpeta se creará pero lo que tendremos en el contenedor es una carpeta vacía. 

