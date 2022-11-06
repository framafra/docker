Mediante el comando ``docker ps`` podemos listar los contenedores en el sistema,tanto parados como en ejecución.

Si ejecutamos solo ``docker ps`` nos indica los que están en ejecución

```bash
$ docker ps
CONTAINER ID   IMAGE   COMMAND              CREATED             STATUS              PORTS                                   NAMES
02e86fdf39bd   httpd   "httpd-foreground"   About a minute ago  Up About a minute   0.0.0.0:8080->80/tcp, :::8080->80/tcp   my-apache-app
```

Mientras si ejecutamos lo siguiente:

```bash
$ docker ps -a
CONTAINER ID   IMAGE     COMMAND                CREATED         STATUS                     PORTS                                   NAMES
02e86fdf39bd   httpd     "httpd-foreground"     8 minutes ago   Up 8 minutes               0.0.0.0:8080->80/tcp, :::8080->80/tcp   my-apache-app
db20a19fbd04   ubuntu    "bash"                 9 minutes ago   Exited (0) 9 minutes ago                                           contenedor1
0f7c3e9e6690   ubuntu    "echo 'Hello world'"   9 minutes ago   Exited (0) 9 minutes ago                                           lucid_goldwasser
```


La información que obtenemos de los contenedores es la siguiente:

- CONTAINER_ID : identificador único del contenedor.
- IMAGE : imagen utilizada para crear el contenedor.
- COMMAND : comando que se lanza al arrancar el contenedor.
- CREATED : cuando se creó el contenedor.
- STATUS : si el contenedor está en marcha o no (indicando cuánto lleva en marcha o cuánto hace que se paró).
- PORTS : redirección de puertos del contenedor.
- NAMES : nombre del contenedor. Se puede generar como parámetro al crear el contenedor, o si no se indica nada, el propio Docker genera un nombre aleatorio.
