En este ejemplo vamos a desplegar con docker-compose la aplicación *Temperaturas*.

Puedes encontrar el fichero `docker-compose.yml` en en este [directorio](https://github.com/josedom24/curso_docker_2022/tree/main/ejemplos/sesion4/ejemplo2) del repositorio. 


En este caso el fichero `docker-compose.yml` puede tener esta forma:

```yaml
version: '3.1'
services:
  frontend:
    container_name: temperaturas-frontend
    image: iesgn/temperaturas_frontend
    restart: always
    ports:
      - 80:3000
    depends_on:
      - backend
  backend:
    container_name: temperaturas-backend
    image: iesgn/temperaturas_backend
    restart: always
```

Para crear el escenario:

```bash
$ docker-compose up -d
Creating network "temperaturas_default" with the default driver
Creating temperaturas-backend ... done
Creating temperaturas-frontend ... done

```

Para listar los contenedores:

```bash
$ docker-compose ps
---------------------------------------------------------------------
temperaturas-backend    python3 app.py   Up      5000/tcp            
temperaturas-frontend   python3 app.py   Up      0.0.0.0:80->3000/tcp
```