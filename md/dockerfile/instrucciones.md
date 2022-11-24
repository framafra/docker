Alguna de las principales instrucciones son:

* **FROM**: Sirve para especificar la imagen sobre la que voy a construir la mía. Ejemplo: `FROM php:7.4-apache`.
* **LABEL**: Sirve para añadir metadatos a la imagen mediante clave=valor. Ejemplo: `LABEL company=iesjaumeII`.
* **COPY**: Para copiar ficheros desde mi equipo a la imagen. Esos ficheros deben estar en el mismo contexto (carpeta o repositorio). Su sintaxis es `COPY [--chown=<usuario>:<grupo>] src dest`. Por ejemplo: `COPY --chown=www-data:www-data myapp /var/www/html`.
* **ADD**: Es similar a COPY pero tiene funcionalidades adicionales como especificar URLs y tratar archivos comprimidos.
* **RUN**: Ejecuta una orden creando una nueva capa. Su sintaxis es `RUN orden` / `RUN ["orden","param1","param2"]`. Ejemplo: `RUN apt update && apt install -y git`. En este caso es muy importante que pongamos la opción `-y` porque en el proceso de construcción no puede haber interacción con el usuario.
* **WORKDIR**: Establece el directorio de trabajo dentro de la imagen que estoy creando para posteriormente usar las órdenes RUN,COPY,ADD,CMD o ENTRYPOINT. Ejemplo: `WORKDIR /usr/local/apache/htdocs`.
* **EXPOSE**: Nos da información acerca de qué puertos tendrá abiertos el contenedor cuando se cree uno en base a la imagen que estamos creando. *Es meramente informativo*.  Ejemplo: `EXPOSE 80`.
* **USER**: Para especificar (por nombre o UID/GID) el usuario de trabajo para todas las órdenes RUN,CMD Y ENTRYPOINT posteriores. Ejemplos: `USER framafra` / `USER 1001:10001`.
* **ARG**: Para definir variables para las cuales los usuarios pueden especificar valores a la hora de hacer el proceso de build mediante el flag `--build-arg`. Su sintaxis es `ARG nombre_variable` o `ARG nombre_variable=valor_por_defecto`. Posteriormente esa variable se puede usar en el resto de la órdenes de la siguiente manera `$nombre_variable`. Ejemplo: `ARG usuario=www-data`. No se puede usar con ENTRYPOINT Y CMD.
* **ENV**: Para establecer variables de entorno dentro del contenedor. Puede ser usado posteriormente en las órdenes RUN añadiendo $ delante de el nombre de la variable de entorno. Ejemplo: `ENV WEB_DOCUMENT_ROOT=/var/www/html`. No se puede usar con ENTRYPOINT Y CMD.
* **ENTRYPOINT**: Para establecer el ejecutable que se lanza siempre  cuando se crea el contenedor  con `docker run`, salvo que se especifique expresamente algo diferente con el flag `--entrypoint`. Su síntaxis es la siguiente: `ENTRYPOINT <command>` / `ENTRYPOINT ["executable","param1","param2"]`. Ejemplo: `ENTRYPOINT ["/usr/sbin/apache2ctl","-D","FOREGROUND"]`.
* **CMD**: Para establecer el ejecutable por defecto (salvo que se sobreescriba desde la orden `docker run`) o para especificar parámetros para un `ENTRYPOINT`. Si tengo varios sólo se ejecuta el último. Su sintaxis es `CMD param1 param2` / `CMD ["param1","param2"]` / `CMD["command","param1"]`. Ejemplo: `CMD [“-c” “/etc/nginx.conf”]`  / `ENTRYPOINT [“nginx”]`.
*  **LABEL**: permite establecer metadatos dentro de la imagen mediante etiquetas.


## Explicación de algunas instrucciones

### EXPOSE
En primer lugar, repasamos la diferencia entre exponer y publicar puertos en Docker:

- Si no se expone ni publica un puerto, este sólo es accesible desde el interior del contenedor.
- Exponer un puerto, indica que ese puerto es accesible tanto dentro del propio contenedor como por otros contenedores, pero no desde fuera (incluido el anfitrión).
- Publicar un puerto, indica que el puerto es accesible desde fuera del contenedor, por lo cual debe asociarse a un puerto del anfitrión.

La opción EXPOSE nos permite indicar los puertos por defecto expuestos que tendrá un contenedor basado en esta imagen. Es similar a la opción “--expose” de “docker run” (y de paso, recordamos que “docker run” con “-p” los publica). Por ejemplo, para exponer 80 443 y 8080 indicaremos:

    EXPOSE 80 443 8080

### ADD/COPY
ADD y COPY son comandos para copiar ficheros de la máquina anfitrión al nuevo contenedor. Se recomienda usar COPY, excepto que queramos descomprimir un “zip”, que ADD permite su descompresión.  
Más información sobre la diferencia entre ADD y COPY: [https://nickjanetakis.com/blog/docker-tip-2-the-difference-between-copy-and-add-in-a-dockerile](https://nickjanetakis.com/blog/docker-tip-2-the-difference-between-copy-and-add-in-a-dockerile)

Ejemplo de uso de ADD:

    ADD ./mifichero.zip /var/www/html

Descomprimirá el contenido de “mifichero.zip” en el directorio destino de la nueva imagen.

Ejemplo de uso de COPY:

    COPY ./mifichero.zip /var/www/html

o incluso accediendo desde la web.

    COPY http://miservidor.commifichero.zip /var/www/html

En este caso, copiará el fichero “mifichero.zip” en el directorio destino de la nueva imágen.


### ENTRYPOINT
Por defecto, los contenedores Docker están configurados para que ejecuten los comandos que se lancen mediante “/bin/sh -c”. Dicho de otra forma, los comandos que lanzábamos, eran parámetros para  “/bin/sh -c”. Podemos cambiar qué comando se usa para esto con ENTRYPOINT. Por ejemplo:

    ENTRYPOINT ["cat"]
    CMD ["/etc/passwd"]

Indicaremos que los comandos sean lanzados con “cat”. Al lanzar el comando “/etc/passwd”, realmente lo que haremos es que se lanzará “cat /etc/passwd”.

### USER
Por defecto, todos los comandos lanzados en la creación de la imagen se ejecutan con el usuario root (usuario con UID=0). Para poder cambiar esto, podemos usar el comando USER, indicando el nombre de usuario o UID con el que queremos que se ejecute el comando. Por ejemplo:

    USER paco
    CMD id

Mostrará con el comando “id” el uid y otra información del usuario paco.


### WORKDIR
Cada vez que expresamos el comando WORKDIR, estamos cambiando el directorio de la imagen donde ejecutamos los comandos. Si este directorio no existe, se crea. Por ejemplo:

    WORKDIR /root
    CMD mkdir tmp
    WORKDIR /var/www/html
    CMD mkdir tmp

Creará la carpeta “tmp” tanto en “/root” como en “/var/www/html”. Si los directorios “/root” o “/var/www/html” no hubieran existido, los hubiera creado.


### ENV
El comando ENV nos permite definir variables de entorno por defecto en la imagen.
    
    ENV v1=”valor1” v2=”valor2”

Esto definirá las variables de entorno “v1” y “v2” con los valores “valor1” y “valor2”.


!!! note "DockerFile"
    Para una descripción completa sobre el fichero `Dockerfile`, puedes acceder a la [documentación oficial](https://docs.docker.com/engine/reference/builder/).