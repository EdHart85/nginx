<h1 align="center">Nginx Config 

</h1>
<p align="center">Some Nginx configuration examples that might work for most cases.</p>

<!--ts-->
* [Enviroment](#enviroment)
* [Nginx installation and initial setup](#installation)
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

<h2>Nginx installation and initial setup</h2>

-Install nginx using 'apt':
```bash
apt update
apt install nginx
```

-Create a directory for your virtualhosts certificates:
```bash
mkdir /etc/nginx/certs
```

-Adjust permissions:
```bash
chown -R root:root /etc/nginx/certs
chmod 400 /etc/nginx/certs
```

<h2>nginx.conf</h2>

This nginx.conf file should work well for most common enviroments. I recommend you to take a look at all parameters used and what it does. I tried to comment it as much and as clear as I could. Nginx official documentation (https://nginx.org/en/docs/) can help you out too.nginx

<h2>virtualhost_template</h2>

I'll try to descrive below the most important aspects of the virtualhost template file. Once again I tried to comment it as much and as clear as I could.

<h3>server_name</h3>

<h3>dhparam</h3>

You can learn more about Diffie-Hellman group parameters here: https://wiki.openssl.org/index.php/Diffie-Hellman_parameters
Your Diffie-Hellman group parameters should match the key size used in the server's certificate. If you use a 2048-bit RSA prime in the server's certificate, then use a 2048-bit Diffie-Hellman group for key agreement.

I would recommend you to use a different DH parameter file for which virtualhost on your server for increase security.
You can generate a DH parameter file using the following command line:

```bash
openssl dhparam -out /etc/nginx/certs/mywebsite_dhparam.pem 2048
chmod 400 /etc/nginx/certs/mywebsite_dhparam.pem
```

Don't forget to secure the file permissions:
```bash
chmod 400 /etc/nginx/certs/mywebsite_dhparam.pem
```

<h3>tls</h3>

<h3>Friendly URLs</h3>

<h3>PHP-FPM version</h3>
