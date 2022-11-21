Podemos subir una imágen a un repositorio (por defecto Docker Hub). Para ello, primero debemos crearnos una cuenta en [Docker Hub](https://hub.docker.com/)

Una vez tenganos cuenta tenemos que logearnos a ella a traves de la consola de nuestro equipo mediante el comando:

    docker login


almacenando imagen local en repositorio Docker Hub
En primer lugar, deberemos loguearnos mediante consola al repositorio mediante el comando
docker login

Una vez logueado, debemos hacer un “commit” local de la imagen, siguiendo la estructura vista en el punto anterior. Un ejemplo podría ser:

    docker commit -a "paco" -m "Apache con nano" IDCONTENEDOR framafra/apachenano:latest

Y por último, para subirlo  este commit local, debemos subirlo usando “docker push”

    docker push framafra/apachenano

Una vez hecho eso, si la imagen es pública, cualquiera podrá descargarla y crear contenedores usando “docker pull” o “docker run”.

Más información de los comandos:

-   Docker login [https://docs.docker.com/engine/reference/commandline/login/]( https://docs.docker.com/engine/reference/commandline/login/)
-   Docker push [https://docs.docker.com/engine/reference/commandline/push/](https://docs.docker.com/engine/reference/commandline/push/)

