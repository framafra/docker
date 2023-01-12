Muchas veces necesitamos ejecutar varios contenedores para que nuestra aplicación funcione (por ejemplo al desplegar una página web dinámica, donde utilizamos un contenedor para la BBDD y otro para el servidor web). 
Es decir:

* Necesitamos varios servicios para que la aplicación funcione: Partiendo del principio de que cada contenedor ejecuta un sólo proceso, si necesitamos que la aplicación use varios servicios (web, base de datos, proxy inverso, ...) cada uno de ellos se implementará en un contenedor.
* Si tenemos construida nuestra aplicación con microservicios, cada uno de ellos se podrá implementar en un contenedor independiente.

Por tanto, el proceso de poner en marcha varios contenedores es tedioso, ya que usualmente debemos levantar “a mano” esos contenedores, respetando el orden de levantado, etc.  

**Docker Compose** es una herramienta para definir y ejecutar aplicaciones multi-contenedor. Con un solo comando podremos crear e iniciar todos los servicios que necesitamos para nuestra aplicación.

Los casos de uso más habituales para docker-compose son:

* Entornos de desarrollo
* Entornos de testeo automáticos (integración contínua)
* Despliegue en host individuales (no clusters)

Compose tiene comandos para manejar todo el ciclo de vida de nuestra aplicación:

* Iniciar, detener y rehacer servicios.
* Ver el estado de los servicios.
* Visualizar los logs.
* Ejecutar un comando en un servicio.

Para utilizar Docker Compose, vamos a crear en un fichero llamado **`docker-compose.yaml`**, y en él definiremos los contenedores y las características de los mismo que deseamos utilizar. Posteriormente, mediante la utilidad `docker-compose` gestionaremos los contenedores.

## Ventajas de usar docker-compose

* Hacer todo de manera **declarativa** para que no tenga que repetir todo el proceso cada vez que construyo el escenario.
* Poner en funcionamiento todos los contenedores que necesita mi aplicación de una sola vez y debidamente configurados.
* Garantizar que los contenedores **se arrancan en el orden adecuado**. Por ejemplo: mi aplicación no podrá funcionar debidamente hasta que no esté el servidor de bases de datos funcionando en marcha.
* Asegurarnos de que hay **comunicación** entre los contenedores que pertenecen a la aplicación.

<br>

Más información en [https://docs.docker.com/compose/](https://docs.docker.com/compose/) 