<h1 align="center">Nginx Config 

</h1>
<p align="center">Some Nginx configuration examples that might work for most cases.</p>

<!--ts-->
* [Enviroment](#enviroment)
* [nginx.conf](#nginxconf)
* [virtualhost_template](#virtualhosttemplate)
  * [server_name](#server_name)
  * [dhparam](#dhparam)
  * [tls](#tls)
  * [Friendly URLs](#friendlyurls)
  * [PHP-FPM version](#phpfpm)
<!--te-->

<h2>Enviroment</h2>

I'm using Debian (best GNU/Linux distro, if you ask me!), so everything here will assume that you are using it too.
Tested on Nginx 1.14.2 / Debian GNU/Linux 10 (buster)

<h2>nginx.conf</h2>

This nginx.conf file should work well for most common enviroments. I recommend you to take a look at all parameters used and what it does. I tried to comment as much and as clear as I could. Nginx official documentation (https://nginx.org/en/docs/) can help you out too.nginx
