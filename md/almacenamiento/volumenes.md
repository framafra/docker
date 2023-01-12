## Los contenedores son efímeros
Por defecto, todos los archivos que se crean dentro de un contenedor se almacenan en la última capa del sistema de archivos (la capa de lectura/escritura), esto quiere decir que los datos que tenemos en esta capa se perderán cuando el contenedor se elimine y no podremos compartirlos con otros contenedores.  
Es decir, **los contenedores son efímeros**, puesto que, los ficheros, datos y configuraciones que creamos en los contenedores sobreviven a las paradas de los mismos pero, sin embargo, son destruidos si el contenedor es destruido. 

## Los datos en los contenedores

![docker](../images/types-of-mounts.png)

Ante la situación anteriormente descrita Docker nos proporciona varias soluciones para persistir los datos de los contenedores:

* Los **volúmenes docker**.
* Los **bind mount**
* Los **tmpfs mounts**: Almacenan en memoria la información. (No lo vamos a ver)

