<h1 align="center">Nginx Configuration

</h1>
<p align="center">Nginx configuration examples that might work for most cases that use PHP-FPM.</p>

<!--ts-->
* [Enviroment](#enviroment)
* [Nginx installation and initial setup](#installation)
* [nginx.conf](#nginxconf)
* [virtualhost_template](#virtualhosttemplate)
  * [Virtualhost Name](#server_name)
  * [DH parameters](#dhparam)
  * [Cryptographic ciphers and protocols](#tls)
  * [Friendly URLs](#friendlyurls)
  * [PHP-FPM version](#phpfpm)
<!--te-->

<h2>Enviroment</h2>

I'm using Debian (best GNU/Linux distro, if you ask me!), so everything here will assume that you are using it too.

Tested on Nginx 1.14.2 / Debian GNU/Linux 10 (buster)


<h2>Nginx installation and initial setup</h2>

-Install Nginx using 'apt':
```bash
apt update
apt install nginx
```
Obs: At this time I'll not describe PHP-FPM installation.

-Create a directory for your virtualhosts certificates:
```bash
mkdir /etc/nginx/certs
```

-Place your certificates files in this directory and adjust permissions:
```bash
mv /home/user/mycertificate.xyz /etc/nginx/certs
chown -R root:root /etc/nginx/certs
chmod -R 400 /etc/nginx/certs
```


<h2>nginx.conf</h2>

This nginx.conf file should work well for most common enviroments.

I recommend you to take a look at all parameters used and what it does. I tried to comment it as much and as clear as I could. Nginx official documentation (https://nginx.org/en/docs/) can help you out, too.


<h2>virtualhost_template</h2>

Here we will describe the most important aspects of the 'virtualhost_template' file. However, it's recommended to check the entire file.


<h3>server_name</h3>

Regarding your virtualhost name, remember to adjust the following parameters:
server_name (both occurences)

root

ssl_certificate

ssl_certificate_key

ssl_trusted_certificate

resolver

ssl_dhparam

access_log

error_log


<h3>dhparam</h3>

You can learn more about Diffie-Hellman group parameters here: https://wiki.openssl.org/index.php/Diffie-Hellman_parameters

Your Diffie-Hellman group parameters should match the key size used in the server's certificate. If you use a 2048-bit RSA prime in the server's certificate, then use a 2048-bit Diffie-Hellman group for key agreement.

I would recommend you to use a different DH parameter file for which virtualhost on your server for increase security.

You can generate a DH parameter file using the following command line (it may take several minutes to complete):

```bash
openssl dhparam -out /etc/nginx/certs/mywebsite_dhparam.pem 2048
chmod 400 /etc/nginx/certs/mywebsite_dhparam.pem
```

Don't forget to secure the file permissions:
```bash
chmod 400 /etc/nginx/certs/mywebsite_dhparam.pem
```


<h3>Cryptographic ciphers and protocols</h3>
I strongly recommend using only TLSv1.2 and TLS1.3 as of now there are no know vulnerabilities in TLSv1.3 and TLSv1.2 is very secure with the right configuration. Older TLS versions (1.1 and 1.0) should not be used as they have many security vulnerabilities that can be exploit by an attacker.

After a lot of reading and testing, I came up with a nice and secure set of encryption algorithms that preserve compatibility for most cases.

Once you are done with your virtualhost configuration, you can test it here: https://www.ssllabs.com/ssltest/


<h3>Friendly URLs</h3>

Nginx configuration varies if your virtualhost uses friendly url's. Check the virtualhost_template file and choose the configuration that suits each case.


<h3>PHP-FPM version</h3>

You may have to adapt the parameter 'fastcgi_pass' according to your PHP-FPM version.
