El fichero **“docker-compose.yml”** es un fichero en formato YAML que definirá los contenedores que queremos crear y el comportamiento de los mismos.    
Lo habitual, es tener ese fichero en la raíz de nuestro proyecto.

### Formato YAML
YAML es el acrónimo recursivo de “YAML Ain't Markup Language”, que en castellano significa, “YAML no es un lenguaje de marcas”. Más información en [https://es.wikipedia.org/wiki/YAML](https://es.wikipedia.org/wiki/YAML)

YAML es a efectos prácticos una forma de definir información utilizando formato texto. Funciona de forma similar a XML o JSON.

El uso de YAML dentro de “Docker Compose” es sencillo y fácilmente entendible con cada uno de los ejemplos. 

### Contenido del archivo 'docker-compose.yml'  
El contenido del archivo docker-compose.yml sigue unas especificaciones. La última especificación completa es la de la versión 3.9. Estas especificaciones están definicas en [ https://docs.docker.com/compose/compose-file/compose-file-v3/](https://docs.docker.com/compose/compose-file/compose-file-v3/)

Los parámetros más importantes de dicha especificación de describen a continuación:

- **version**.- Indica la versión de la especificación del fichero “docker-compose.yml” no es necesario ponerlo desde la versión 1.27.0 de “Docker Compose”.
- **services**.- Array asociativo con las diferentes plantillas de cada contenedor que queremos crear.
- **build**.- Sirve para contruir la imagen de un contenedor a partir de un "Dockerfile",  la forma más habitual de usarla es indicar en qué directorio está nuestro nuestro “Dockerfile” de la forma “build: ./directorio”. Para más detalles [https://docs.docker.com/compose/compose-file/compose-file-v3/#build](https://docs.docker.com/compose/compose-file/compose-file-v3/#build),
- **command**.- Sobreescribe el comando por defecto a la imagen. Se usa de la forma “command: /bin/bash”.
- **container_name**.- Especifica el nombre de contenedor (si no, se generará automáticamente). Se usa de la forma “container_name: micontenedor”
- **depends_on**.- Indica que el contenedor de la plantilla depende de otro que se haya creado previamente, puesto que los contenedores se crean de forma secuencial a cómo están declarados en el fichero docker-compose.yml. Del mismo modo los contenedores se detienen en orden inverso a cómo se han declarado. Se puden ver ejemplos en [https://docs.docker.com/compose/compose-file/compose-file-v3/#depends_on](https://docs.docker.com/compose/compose-file/compose-file-v3/#depends_on)
- **env_file y environment**.- Permite definir variables de entorno en la plantilla del contenedor.
    - env_file especifica un fichero o lista de ficheros donde están definidas las variables de entorno, similar a “env_file: .env”
    - environment especifica una lista de variables de entorno con su valor. <br>Ejemplos en [https://docs.docker.com/compose/compose-file/compose-file-v3/#environment](https://docs.docker.com/compose/compose-file/compose-file-v3/#environment)
- **expose / ports**.- Permite definir un conjunto de puertos que estarán abiertos en el contenedor. Ejemplos en [https://docs.docker.com/compose/compose-file/compose-file-v3/#expose](https://docs.docker.com/compose/compose-file/compose-file-v3/#expose) y en [https://docs.docker.com/compose/compose-file/compose-file-v3/#ports](https://docs.docker.com/compose/compose-file/compose-file-v3/#ports).
- **image**.- Específica la imagen en la que se basa el contenedor. No es necesario cuando se especifica a partir de un “Dockerfile”.
- **network_mode**: especifica el modo de red, de forma similar al parámetro --network de Docker. Los modos soportados se detallan en el siguiente enlace [https://docs.docker.com/compose/compose-file/compose-file-v3/#network_mode] (https://docs.docker.com/compose/compose-file/compose-file-v3/#network_mode)
- **networks**.- Define las redes a crear para poner en marcha nuestros contenedores. Ejemplos en [https://docs.docker.com/compose/compose-file/compose-file-v3/#networks](https://docs.docker.com/compose/compose-file/compose-file-v3/#networks)
- **restart**.- Indica cuando debe reiniciarse el contenedor. El valor por defecto es “no” (no se reinicia). Otros valores soportados son “always” (se reinicia cuando el contenedor se para) y “on-failure” (se reinicia si el contenedor se para y devuelve un valor de salida distinto de cero) y “unless-stoped” (se reinicia siempre, excepto si el contenedor es parado manualmente con “docker stop”). Ejemplos [https://docs.docker.com/compose/compose-file/compose-file-v3/#restart](https://docs.docker.com/compose/compose-file/compose-file-v3/#restart)
- **volumes**.- establece una lista de volúmenes, ya sea en formato “bind mount” o volumen Docker. Si quieres reutilizar un volumen entre distintas plantillas, además debes definir la variable “volumes” fuera de las plantillas de contenedores. Ejemplos [https://docs.docker.com/compose/compose-file/compose-file-v3/#volumes](https://docs.docker.com/compose/compose-file/compose-file-v3/#volumes)


### Ejemplo
A continuación se muestra un ejemplo de un fichero `docker-compose.yml`

```
version: '3.8'
services:
  app:
    container_name: letschat
    image: sdelements/lets-chat
    restart: always
    environment:
      LCB_DATABASE_URI: mongodb://mongo/letschat
    ports:
      - 80:8080
    depends_on:
      - db
  db:
    container_name: mongo
    image: mongo
    restart: always
    volumes:
      - /opt/mongo:/data/db
```

