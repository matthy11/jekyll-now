---
layout: post
title: Emepezando con Docker
---
<!-- Asi se ponen las fotos en Mackdown
![foto_personal](https://raw.githubusercontent.com/matthy11/matthy11.github.io/master/images/foto1.jpg)
-->

***

# Iniciando con Docker en Centos

### Borrar todo lo que pueda tener de docker con anterioridad

~~~

- sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine'  

~~~

### Instalar Docker desde repositorios  

~~~

- sudo yum install -y yum-utils
  sudo yum-config-manager \
    --add-repo \
  https://download.docker.com/linux/centos/docker-ce.repo

~~~

### Instalar Docker Engine  

~~~

-  sudo yum install docker-ce docker-ce-cli containerd.io

~~~

### Iniciar Docker  

~~~

- sudo systemctl start docker

~~~

### Para verificar la correcta instalación de Docker ejecutamos un Hello-World  

~~~

- sudo docker run hello-world

~~~

### Desintalar Docker  

~~~

- sudo yum remove docker-ce docker-ce-cli containerd.io

~~~

### Para eliminar imagenes, volumenes y cotenedores (no se eliminar automáticamente)

~~~

- sudo rm -rf /var/lib/docker
  sudo rm -rf /var/lib/containerd

~~~
