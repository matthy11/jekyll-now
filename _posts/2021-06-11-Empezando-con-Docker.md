---
layout: post
title: Emepezando con Docker
---
<!-- Asi se ponen las fotos en Mackdown
![foto_personal](https://raw.githubusercontent.com/matthy11/matthy11.github.io/master/images/foto1.jpg)
-->

***

# Iniciando con Docker

### Borrar todo lo que pueda tener de docker con anterioridad

<Remove>

-  sudo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine  

</Remove>


### Instalar Docker desde repositorios  

- sudo dnf -y install dnf-plugins-core
  sudo dnf config-manager \
    --add-repo \
  https://download.docker.com/linux/fedora/docker-ce.repo


### Instalar Docker Engine  

-  sudo dnf install docker-ce docker-ce-cli containerd.io


### Iniciar Docker  

- sudo systemctl start docker


### Para verificar la correcta instalación de Docker ejecutamos un Hello-World  

- sudo docker run hello-world


### Desintalar Docker  

- sudo dnf remove docker-ce docker-ce-cli containerd.io

### Para eliminar imagenes, volumenes y cotenedores (no se eliminar automáticamente)

- sudo rm -rf /var/lib/docker
  sudo rm -rf /var/lib/containerd

