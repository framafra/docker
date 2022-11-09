# Instalación de docker
Existe dos versiones de Docker, una libre y otra que no lo es.

Nos ocuparemos exclusivamente de la primera: [Docker CE (Community Edition)](https://docs.docker.com/install/).

Docker CE está disponible para los siguientes sistemas GNU/Linux: CentOS, Debian, Fedora y Ubuntu.

No todas están en múltiples arquitecturas, pero sí todas soportan _x86\_64/amd64_. Si tienes otra arquitectura u otro sistema es mejor que uses una máquina virtual para arrancar una distribución compatible.

Para más información sobre sistemas privativos soportados, leer la sección de [plataformas soportadas](https://docs.docker.com/install/#supported-platforms) de la documentación oficial.

## Instalación

Debido a que, dependiendo de la distribución, la forma de instalarlo difiere, es mejor consultar la documentación oficial para saber como instalar Docker en tu máquina.

* Ubuntu: [https://docs.docker.com/install/linux/docker-ce/ubuntu/](https://docs.docker.com/install/linux/docker-ce/ubuntu/)
* Debian: [https://docs.docker.com/install/linux/docker-ce/debian/](https://docs.docker.com/install/linux/docker-ce/debian/)
* CentOS: [https://docs.docker.com/install/linux/docker-ce/centos/](https://docs.docker.com/install/linux/docker-ce/centos/)
* Fedora: [https://docs.docker.com/install/linux/docker-ce/fedora/](https://docs.docker.com/install/linux/docker-ce/fedora/)

!!! note Nota
    
    Es posible instalar Docker engine desde el repositorio oficial de Ubuntu, pero <u>no está recomendado</u> ya que instala versiones antiguas.

Es recomendable desinstalar las versiones antiguas antes de realizar la instalación y así evitar que pudiesen haber conflictos.
En sistemas Ubuntu, para eliminar las versiones antiguas, podemos ejecutar la instrucción:

    sudo apt-get remove docker docker-engine docker.io containerd runc


!!! note "Comprobar la versión instalada."

        sudo docker version

## Configuración del usuario

Si estamos usando _Docker_ en nuestro ordenador personal, podemos configurar nuestro usuario para usar el cliente sin tener que poner _sudo_ delante. Para ello ejecuta lo siguiente:

        sudo usermod -aG docker $USER

Para que los nuevos permisos surtan efecto, debes cerrar y volver a abrir la sesión. Para problemas relacionados con los permisos visitad [la página del manual oficial](https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user).



## Activar/desactivar arranque al inicio
Para indicar que el servicio Docker se inicie al arrancar la máquina, podemos indicarlo mediante los siguientes comandos:
   
    sudo systemctl enable docker.service
    sudo systemctl enable containerd.service

Si lo que queremos es deshabilitar este arranque automático, podemos usar:
   
    sudo systemctl disable docker.service
    sudo systemctl disable containerd.service

Para iniciar/parar/reiniciar los servicios manualmente, podemos usar:
    
    sudo systemctl start/stop/restart docker.service
    sudo systemctl start/stop/restart containerd.service

