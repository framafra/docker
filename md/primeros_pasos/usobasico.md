Usar Docker consiste en pasar una cadena de opciones y comandos seguidos de argumentos, la sintaxis sería la siguiente:

    $docker [option] [command] [arguments]

Para ver todos los subcomandos disponibles podemos ejecutar:

    $docker

Si queremos sabe que realiza un comando en concreto, tendremos que ejecutar:

    $docker docker -subcommand --help

“docker -subcommand” puede ser cualquiera de los mostrados por $docker.

Como hemos visto anteriormente los contenedores Docker se forman a partir de imágenes de Docker.

Por defecto, Docker extrae estas imágenes de **Docker Hub**, recordemos que es un registro de Docker administrado por Docker, la empresa responsable del proyecto Docker.

Cualquier persona es capaz de guardar sus imágenes Docker en Docker Hub, por lo tanto, la mayoría de aplicaciones y distribuciones Linux que necesitaremos tendrán las imágenes guardadas.
