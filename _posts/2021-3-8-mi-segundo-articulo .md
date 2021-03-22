---
layout: post
title: GIT
---

== Instalación ==

Inatalar los paquetes de git:

{{{
$ yum install git
}}}

Instalar paquetes complementarios (opcional):

{{{
$ yum install gitg gedit-plugins gedit-plugin-git
}}}

== Servidor Git ==

Los repositorios Git para TI están centralizados en el sevidor Gogs:

{{{
http://gogs1.servicios.bbr
}}}

== Comandos útiles de git ==

 * Clonar un repositorio en la máquina local:

{{{
$ git clone http://gogs1.servicios.bbr/dmedina/tutorial-git
}}}

 * Obtener el estado del repositorio:

{{{
$ git status
}}}

 * Agregar un archivo nuevo o que fue modificado al stage de git para el próximo commit:

{{{
$ git add <archivo-nuevo>
}}}

 * Hacer commit de los cambios en el repositorio:

{{{
$ git commit -m "Mensaje descriptivo del commit"
}}}

 * Ver el log de commits:

{{{
$ git log
}}}

 * Ver lel log en modo resumido:

{{{
$ git log --pretty=oneline
}}}

 * Ver las ramas (branches) que tengo localmente:

{{{
$ git branch
}}}

 * Crear una nueva rama llamada ''testing'':

{{{
$ git branch testing
}}}

 * Cambiar de rama:

{{{
$ git checkout testing
}}}

 * Ver diferencias entre un archivo modificado y la última versión del repositorio:

{{{
$ git diff mi-archivo-modificado
}}}

 * Actualizar el repositorio local con las novedades del servidor remoto:

{{{
$ git pull origin
}}}

 * Enviar los cambios (commits) locales de una rama al servidor remoto:

{{{
$ git push origin testing
}}}

 * Unir (merge) dos ramas:

{{{
$ git checkout master   ## Cambiar a la rama que será modificada
$ git merge testing     ## Aplicar a la rama master todas las modificaciones que estén en testing
}}}

 * Descartar cambios realizados a un archivo:

{{{
$ git checkout <archivo>
}}}

 * Listar servidores remotos:

{{{
$ git remote -v
}}}

== Modelos de DB ==
Los modelos de DB están en el repositorio http://gogs1.servicios.bbr/hmolina/modelos-db.

![foto_personal](https://raw.githubusercontent.com/matthy11/matthy11.github.io/master/images/foto1.jpg)



