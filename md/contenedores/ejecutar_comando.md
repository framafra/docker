El comando ``docker exec`` nos permite ejecutar un comando dentro de un contenedor que esté en ese momento en ejecución.ç

La forma sintaxis habitual para utilizar este comando es:

    docker exec [OPCIONES] IDENTIFICADOR/NOMBRE COMANDO [ARGUMENTOS]


Algunos ejemplos de uso, suponiendo un contenedor en marcha llamando “contenedor”:

!!! example "Ejemplo 1"

    Se ejecuta en “background”, gracias al parámetro “-d”, y crea mediante el comando “touch” un fichero “prueba” en “/tmp”.

        docker exec -d contenedor touch /tmp/prueba

!!! example "Ejemplo 2"

    Ejecuta la “shell” bash en nuestra consola (gracias al parámetro “-it” se enlaza la entrada y salida estándar a nuestra terminal). A efectos prácticos, con esta orden accederemos a una “shell” bash dentro del contenedor.

        docker exec -it contenedor bash

!!! example "Ejemplo 3"
    Comando que establece un variable de entorno con el parámetro “-e”. Se enlaza la entrada y salida de la ejecución del comando con “-it”. A efectos prácticos, en esa “shell” estará disponible la variable de entorno “VAR1” con valor 1. Lo podemos probar con ``docker exec -it echo $VAR1``

        docker exec -it -e VAR=1 contenedor bash


La descripción completa del comando “docker exec” la podéis encontrar en [https://docs.docker.com/engine/reference/commandline/exec/](https://docs.docker.com/engine/reference/commandline/exec/)
