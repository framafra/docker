## ¿Qué hace el comando docker run?
Es posiblemente el comando más utilizado. Podríamos decir que este comando crea un contenedor a partir de una imagen y lo arranca.

!!! note "Cuidado!"
        Un error común es creer que “docker run” solo arranca contenedores. Si haces varios “docker run”, estás creando varios contenedores, no arrancando varias veces un contenedor.


La sintaxis sería la siguiente:

    $docker run -opciones --name NombreContenedor

Esta opción crea el contenedor con las características dadas en opciones, que pueden ser:

- -i Mantiene una conexión interactiva con el “standard input”.
- -t Gestiona un “pseudo TTY”.
- -d Ejecuta el contenedor en modo “background” y nos muestra el ID.
- -a Asocia “standard input” o “output” a la sesión abierta.
- -cpus decimal – Número de CPUs asignadas.
- -IP asigna una IP.
- -mac-address string – Asigna una MAC address especial al contenedor.
- -mv Fija un límite de memoria per este contenedor.
- -name Asigna un nombre al contenedor.
- -p Publica los puertos del contenedor en la red asignada.
- -rm Al parar el contenedor, se eliminará automáticamente.
- -tmpfs Monta un directorio en modo tmpfs (temporal, no tiene persistencia).
- -v Monta un directorio en el contenedor con persistencia, puede ser una carpeta del equipo real o un volumen Docker.
- -e Permite crear variable de entorno.

!!! example "Ejemplo"
    Vamos arrancar un contenedor utilizando la imagen de Ubuntu 18.04, en modo interactivo, con nombre “ubu18”, al mismo tiempo se nos abrirá un terminal de bash para interactuar. Para ello ejecutaremos:
            
            docker run --name ubu18 -it ubuntu:18.04 /bin/bash




!!! note "Crear contenedores sin arrancarlos: docker run vs docker create"

    El comando “docker run” crea y arranca un contenedor.
    Si queremos crear un contenedor sin arrancarlo debemos utilizar el comando “docker create”. La descripción completa del comando “docker create” la podéis encontrar en [https://docs.docker.com/engine/reference/commandline/create/](https://docs.docker.com/engine/reference/commandline/create/)