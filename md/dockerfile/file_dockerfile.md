Docker nos permite generar de forma automática nuestras propias imágenes usando el comando “docker build” y los ficheros llamados `Dockerfile`.

Un fichero `Dockerfile` es un **conjunto de instrucciones que serán ejecutadas de forma secuencial para construir una nueva imagen docker**. Cada una de estas instrucciones crea una nueva capa en la imagen que estamos creando. 

Los ficheros Dockerfile pueden crearse con cualquier editor de texto, pero recomendamos el editor
multiplataforma “Visual Studio Code” https://code.visualstudio.com/.
Al instalarlo, si detecta Docker instalado en el sistema, el propio editor nos sugerirá una serie de
plugins que merece la pena instalarlos. En cualquier caso se pueden instalar posterioremente de forma manual, alguno de los más recomendados son: Docker y Dev Containers

La estructura fundamental de un fichero `Dockerfile` suele ser la siguiente:

* Indicamos imagen base con la instrucción FROM
* Añadimos metadatos a la imágen con la instrucción LABEL
* Instrucciones de construcción con instrucciones como RUN, COPY, ADD, WORKDIR.
* Configuración: Variable de entornos, usuarios, puertos: USER, EXPOSE, ENV
* Instrucciones de arranque: CMD, ENTRYPOINT
