Muchas veces necesitamos ejecutar varios contenedores para que nuestra aplicación funcione (por ejemplo al desplegar una página web dinámica, donde utilizamos un contenedor para la BBDD y otro para el servidor web). 
Es decir:

* Necesitamos varios servicios para que la aplicación funcione: Partiendo del principio de que cada contenedor ejecuta un sólo proceso, si necesitamos que la aplicación use varios servicios (web, base de datos, proxy inverso, ...) cada uno de ellos se implementará en un contenedor.
* Si tenemos construida nuestra aplicación con microservicios, cada uno de ellos se podrá implementar en un contenedor independiente.

Por tanto, el proceso de poner en marcha varios contenedores es tedioso, ya que usualmente debemos levantar “a mano” esos contenedores, respetando el orden de levantado, etc.  

*“Docker Compose”** es una aplicación para simplificar la tarea de lanzar múltiples contenedores con una configuración específica y enlazarlos entre sí. Además, “Docker Compose” actúa como un orquestador simple, permitiendo cierto escalado local (aunque con bastantes limitaciones en comparación con otros orquestadores, como Kubernetes).

Para utilizar Docker Compose, vamos a definir el escenario en un fichero llamado `docker-compose.yaml` y vamos a gestionar el ciclo de vida de la aplicación y de todos los contenedores que necesitamos con la utilidad `docker-compose`.

## Ventajas de usar docker-compose

* Hacer todo de manera **declarativa** para que no tenga que repetir todo el proceso cada vez que construyo el escenario.
* Poner en funcionamiento todos los contenedores que necesita mi aplicación de una sola vez y debidamente configurados.
* Garantizar que los contenedores **se arrancan en el orden adecuado**. Por ejemplo: mi aplicación no podrá funcionar debidamente hasta que no esté el servidor de bases de datos funcionando en marcha.
* Asegurarnos de que hay **comunicación** entre los contenedores que pertenecen a la aplicación.

<br>

Más información en [https://docs.docker.com/compose/](https://docs.docker.com/compose/) 