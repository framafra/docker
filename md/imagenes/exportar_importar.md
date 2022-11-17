## Exportar
Si tenemos una imagen local en nuestro sistema, podemos hacer una copia de la misma, ya sea como copia de seguridad o como forma de transportarla a otros sistemas mediante el comando “docker save”.

Por ejemplo se puede hacer de estas dos formas:

    docker save -o copiaSeguridad.tar paco/ubuntumod

o de forma alternativa

    docker save > paco/ubuntumod copiaSeguridad.tar

## Importar
Si queremos importar el fichero para crear una imagen en nuestra máquina, podemos usar ``docker import``. Por ejemplo se puede hacer de estas dos formas:

    docker load -i copiaSeguridad.tar

o de forma alternativa

    docker load < copiaSeguridad.tar

Más información sobre los comandos:

- Docker save: [https://docs.docker.com/engine/reference/commandline/save/](https://docs.docker.com/engine/reference/commandline/save/)
- Docker load: [https://docs.docker.com/engine/reference/commandline/load/](https://docs.docker.com/engine/reference/commandline/load/)
