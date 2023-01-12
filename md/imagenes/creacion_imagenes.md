El sistema de imágenes de Docker funciona como un control de versiones por capas, de forma similar a la herramienta “git” para control de versiones. Podemos entender que un contenedor es como una “capa temporal” de una imagen, por lo cual, podemos hacer un “commit” y convertir esa “capa temporal” en una imagen. La sintaxis más habitual es la siguiente:
    
    docker commit -a "autor" -m "comentario" ID/NOMBRE-CONTENEDOR usuario/imagen:[version]

Por ejemplo, si tenemos un contenedor con nombre “mi_ubuntu” que simplemente es un contenedor basado en la imagen “ubuntu” en el que se ha instalado un programa y hacemos:

    docker commit -a "paco" -m "Ubuntu modificado" IDCONTENEDOR paco/ubuntumod:22

y tras ello, comprobamos las imágenes con

    docker images

observamos lo siguiente:

```
paco@paco-xubuntu:~$ sudo docker commit -a "paco" -m "Ubuntu modificado" mi_ubuntu paco/ubuntumod:22
sha256:cb4889c722bed0a38dcdf3c7a7272b0a26d4ef3e9a4d5c18752601c75204b2fa

paco@paco-xubuntu:~$ sudo docker images
REPOSITORY          TAG          IMAGE ID         CREATED             SIZE
paco/ubuntumod      22           cb4889c722be     25 seconds ago      123MB
ubuntu                 latest       a8780b506fa4     12 days ago         77.8MB


```

Ahora ya podríamos crear nuevos contenedores con esa imagen, usando por ejemplo:

    docker run -it paco/ubuntumod:22

Si quisiéramos añadir una nueva etiqueta a la imagen, como “latest”, podemos usar el comando “docker tag”, teniendo en cuenta que una misma imagen puede tener varias etiquetas:

    docker tag paco/ubuntumod:22 paco/ubuntumod:latest

Para eliminar una etiqueta, simplemente deberemos borrar la imagen con docker rmi. La imagen se mantendrá mientras al menos tenga una etiqueta. Por ejemplo con:
    
    docker rmi paco/ubuntumod:22

Más información de los comandos en:

- Docker commit [https://docs.docker.com/engine/reference/commandline/commit/](https://docs.docker.com/engine/reference/commandline/commit/)
- Docker tag [https://docs.docker.com/engine/reference/commandline/tag/](https://docs.docker.com/engine/reference/commandline/tag/)