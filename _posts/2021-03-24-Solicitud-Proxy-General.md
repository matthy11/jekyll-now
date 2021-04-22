---
layout: post
title: Solicitud de Proxy General
---
<!-- Asi se ponen las fotos en Mackdown
![foto_personal](https://raw.githubusercontent.com/matthy11/matthy11.github.io/master/images/foto1.jpg)
-->

***

### Primero pedir accesos a IIA

Solicitar accesos a traves de proxy-general


`1) Origen: IP-servidor  
    Destino: IP-proxy  
    Prueto: 3128 /tcp`  


### Agregar IPs a iptables de proxy (10.200.100.5)

Entrar a la ruta de configuración de iptables:

`vim /etc/sysconfig/iptables`

agregar IP de as1 y as2 si es el caso:

EJ:

`-A INPUT -s 10.200.36.20/32  -p tcp  -m state --state NEW -m tcp --dport 3128 -j ACCEPT`
