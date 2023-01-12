El comando docker cp es un comando que nos permite copiar ficheros y directorios del anfitrión a un contenedor o viceversa.

No se permite actualmente la copia de ficheros entre contenedores.

- COPIA CONTENEDOR --> ANFITRIÓN <BR>Copiando el fichero f1.txt que se encuentra en la carpeta /tmp del contenedor con identificador o nombre “idcontainer” al directorio actual de la máquina que ejerce como anfitrión.
        
        $docker cp idcontainer:/tmp/f1.txt ./

- COPIA ANFITRIÓN --> CONTENEDOR<BR>Copiando el fichero f2.txt del directorio actual al directorio /tmp del contenedor.
        
        $docker cp ./f2.txt idcontainer:/tmp