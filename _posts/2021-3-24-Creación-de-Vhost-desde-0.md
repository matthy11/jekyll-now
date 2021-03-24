---
layout: post
title: Creación de Vhost desde 0
---
<!-- Asi se ponen las fotos en Mackdown
![foto_personal](https://raw.githubusercontent.com/matthy11/matthy11.github.io/master/images/foto1.jpg)
-->

### Paso 1 ###

Entrar al servidor de apache que corresponda (web1 y web2 si es el caso), luego se accede a la ruta `/etc/http/conf.d/` para crear el vhost.

#### Ejemplo Basico ####

<VirtualHost *:443> 

        ServerName prod-skc.b2c.bbr.cl
        ServerAlias prod-skc.b2c.bbr.cl
        DocumentRoot "/var/www/skc/"


       #Log
        CustomLog logs/access_log combined
        ErrorLog logs/error_log
        LogFormat "%{JSESSIONID}C | %{ROUTEID}C | %{BALANCER_SESSION_STICKY}e | %{BALANCER_SESSION_ROUTE}e | %{BALANCER_WORKER_ROUTE}e | %{BALANCER_ROUTE_CHANGED}e | %{Set-Cookie}o" balanceador
        CustomLog logs/balanceador_log balanceador
        LogFormat "%t %{Age}o %{cache-status}e %{CACHE_MISS}e \"%r\"" cachelog
        CustomLog /var/log/httpd/cache.log cachelog

        CacheEnable disk /
        CacheIgnoreURLSessionIdentifiers jsessionid JSESSIONID
        CacheIgnoreHeaders Set-Cookie Cookie
        CacheIgnoreCacheControl On
        CacheIgnoreNoLastMod On
        CacheStoreNoStore On
        CacheIgnoreQueryString On
        CacheDefaultExpire 0
        CacheMaxExpire 0


        SecRuleEngine Off

        ProxyRequests Off
        ProxyPreserveHost On

        ProxyPass /tiendaonline/                  balancer://tiendaonline_cluster/tiendaonline/ stickysession=JSESSIONID|jsessionid scolonpathdelim=On
        ProxyPassReverse /tiendaonline/           balancer://tiendaonline_cluster/tiendaonline/

        ProxyPass /tiendaonlineBO                  balancer://bo_cluster/tiendaonlineBO stickysession=JSESSIONID|jsessionid scolonpathdelim=On 
        ProxyPassReverse /tiendaonlineBO           balancer://bo_cluster/tiendaonlineBO 



        #Proxy Balanceo
        #TiendaOnline
        <Proxy balancer://tiendaonline_cluster>
                BalancerMember ajp://10.200.36.22:8009 ttl=20 ping=1 route=1
                BalancerMember ajp://10.200.36.27:8009 ttl=20 ping=1 route=2
                ProxySet stickysession=JSESSIONID
                ProxySet nofailover=On
        </Proxy>

        #BO
        <Proxy balancer://bo_cluster>
                BalancerMember ajp://10.200.36.21:8009 ttl=20 ping=1 route=1
                BalancerMember ajp://10.200.36.26:8009 ttl=20 ping=1 route=2
                ProxySet stickysession=JSESSIONID
                ProxySet nofailover=On
        </Proxy>


        SSLEngine On


        #SSLProtocol all -SSLv2 -SSLv3
	SSLProtocol -all +TLSv1.2
        SSLHonorCipherOrder on
        SSLCipherSuite kEECDH:+kEECDH+SHA:kEDH:+kEDH+SHA:+kEDH+CAMELLIA:kECDH:+kECDH+SHA:kRSA:+kRSA+SHA:+kRSA+CAMELLIA:!aNULL:!eNULL:!SSLv2:!RC4:!DES:!EXP:!SEED:!IDEA:!3DES
 

	SSLCertificateFile /etc/pki/tls/certs/skc/__bbr_cl.crt
	SSLCertificateKeyFile /etc/pki/tls/certs/skc/__bbr_cl.key
        SSLCertificateChainFile /etc/pki/tls/certs/skc/__bbr_cl.ca-bundle
        SSLVerifyClient none

</VirtualHost>

<VirtualHost *:80>

        ServerName prod-skc.b2c.bbr.cl
        ServerAlias prod-skc.b2c.bbr.cl

        ProxyRequests off

        DocumentRoot "/var/www/skc"

        RewriteEngine on
        RewriteCond %{HTTPS} off
        RewriteRule (.*) https://%{HTTP_HOST}%{REQUEST_URI}
        RewriteCond %{SERVER_NAME} =prod.skrental.b2c.bbr.cl
        RewriteRule ^ https://%{SERVER_NAME}%{REQUEST_URI} [END,NE,R=permanent]

</VirtualHost>



### Validación del certificado y creación de DocumentRoot ###

El certificado puede ser de muchas maneras, las más comun es realizar un certificado autofirmado:

`certbot certonly --apache`

Lo cual listará los vhost que tenemos activos en el servidor

#### Ejemplo ####

[root@web2.servicios.bbr ~]# certbot certonly --apache
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache
Starting new HTTPS connection (1): acme-v01.api.letsencrypt.org

Which names would you like to activate HTTPS for?
-------------------------------------------------------------------------------
1: soporte.areaprod.b2b
2: bbrtask.bbr.cl
3: intranet.bbr.cl
4: oid.bbr.cl
5: soporte.bbr.cl
6: redmine.gt.servicios.bbr
-------------------------------------------------------------------------------
Select the appropriate numbers separated by commas and/or spaces, or leave input
blank to select all options shown (Enter 'c' to cancel): 
