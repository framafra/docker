Es importante aclarar algunos conceptos sobre qué son **imágenes** y **contenedores** y cuales son sus características de estos:

**Imágenes**

- La imagen es una plantilla de solo lectura que se utiliza para crear contenedores. A partir de una imagen pueden crearse múltiples contenedores
- Las imágenes, además de tener sus sistema de ficheros predefinido, tienen una serie de parámetros predefinidos (comandos, de variables de entorno, etc.) con valores por defecto y que se pueden personalizar en el momento de crear el contenedor.
- Docker permite crear nuevas imágenes basándose en imágenes anteriores. Se podría decir que una imagen puede estar formada por un conjunto de “capas” que han modificado una imagen base.
- _Al crear una nueva imagen, simplemente estamos añadiendo una capa a la imagen anterior, la que actúa como base._

<br>

**Contenedores**

- Son instancias de una imagen.
- Pueden ser arrancados, parados y ejecutados.
- Cada contenedor Docker posee un identificador único de 64 caracteres, pero habitualmente se utiliza una versión corta con los primeros 12 caracteres. También se les puede dar un nombre.

<br>

!!! example "Símil"
    Un símil para entender estos conceptos: una instalación de una distribución de Linux mediante un DVD.
    
    Ese DVD sería nuestra imagen y el sistema operativo instalado sería el contenedor.