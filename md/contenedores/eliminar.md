Hay diferentes formas de eliminar contenedores dependiendo de cómo lo queramos hacer:

- Si vamos a eliminar un contenedor que está parado previamente.
        
    $docker rm IDENTIFICADOR/NOMBRE

- Si queremos parar todos los contenedores que tenemos y borrarlos, hay que realizar dos pasos:
  
    – Paramos los contenedores (opcional).

        $docker stop $(docker ps -a -q)

    – Borramos todos los contenedores.

        $docker rm $(docker ps -a -q)