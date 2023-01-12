Para arrancar/parar un contenedor ya creado (recordamos, docker run crea y arranca), existen los comandos ``docker start, docker stop y docker restart`` .

La forma más habitual de usar estos comandos, es usar el nombre del comando, seguido del identificador único o nombre asignado al contenedor.

Por ejemplo con identificador:

    $docker start 434d318b3771

o con nombre del contenedor:

    $docker start NombreContenedor01

!!!Note "Cuidado"
    Si cerramos el terminal, Docker continuará en funcionamiento.