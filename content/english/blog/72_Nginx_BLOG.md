---
title: Installing Nginx Server 
author: DannyJRa
date: '2019-05-09'
slug: installing nginx server
categories:
  - R
tags:
  - Shiny
  - Rstudio
  - Linux
hidden: false
image: images/blog/72_Nginx_BLOG.png
share: false
output:
  html_document:
    keep_md: yes
    theme: cerulean
    highlight: tango
    code_folding: show
    toc: yes
    toc_float: yes
  pdf_document:
    number_sections: yes
geometry: margin = 1.2in
fontsize: 10pt
always_allow_html: yes
---


# Installing Nginx Server

![Login](/images/blog/complainer_BLOG.gif) 


## How To Install Nginx on Ubuntu 18.04[^1]

### Introduction
Nginx is one of the most popular web servers in the world and is responsible for hosting some of the largest and highest-traffic sites on the internet. It is more resource-friendly than Apache in most cases and can be used as a web server or reverse proxy.

### Installing Nginx

Install on Ubuntu 18.04 with ...


```bash
sudo apt install nginx
```

### FIrewall (optional)
After accepting the procedure, apt will install Nginx and any required dependencies to your server.

```bash
sudo ufw app list
```

It is recommended that you enable the most restrictive profile that will still allow the traffic you've configured. Since we haven't configured SSL for our server yet in this guide, we will only need to allow traffic on port 80.

You can enable this by typing:

```bash
sudo ufw allow 'Nginx HTTP'
```


You can verify the change by typing:

```bash
sudo ufw status
```

```
## Status: inactive
```

### Check Nginx

Now, we can check the status for NGINX. Execute the below command to check NGINX Status


```bash
systemctl status nginx
```

```
## ● nginx.service - A high performance web server and a reverse proxy server
##    Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
##    Active: active (running) since Mon 2019-05-13 10:55:40 CEST; 16min ago
##      Docs: man:nginx(8)
##   Process: 18553 ExecStop=/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx.pid (code=exited, status=0/SUCCESS)
##   Process: 18571 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
##   Process: 18554 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
##  Main PID: 18574 (nginx)
##     Tasks: 3 (limit: 4915)
##    CGroup: /system.slice/nginx.service
##            ├─18574 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
##            ├─18578 nginx: worker process
##            └─18579 nginx: worker process
```



Note: You can also use your domain if it is pointing to the server IP.

#TODO: start-page screenshot

### Setting Up Server Blocks (Recommended)

When using the Nginx web server, server blocks (similar to virtual hosts in Apache) can be used to encapsulate configuration details and host more than one domain from a single server. We will set up a domain called example.com, but you should replace this with your own domain name. To learn more about setting up a domain name with DigitalOcean, see our Introduction to DigitalOcean DNS.

Nginx on Ubuntu 18.04 has one server block enabled by default that is configured to serve documents out of a directory at /var/www/html. While this works well for a single site, it can become unwieldy if you are hosting multiple sites. Instead of modifying /var/www/html, let's create a directory structure within /var/www for our example.com site, leaving /var/www/html in place as the default directory to be served if a client request doesn't match any other sites.

Create the directory for example.com as follows, using the -p flag to create any necessary parent directories:


```bash

sudo mkdir -p /var/www/raschadvisory.com/html

```


Next, assign ownership of the directory with the $USER environment variable:


```bash

sudo chown -R danny:danny /var/www/raschadvisory.com/html

```

The permissions of your web roots should be correct if you haven't modified your umask value, but you can make sure by typing:

```bash

sudo chmod -R 755 /var/www/raschadvisory.com

```

Next, create a sample index.html page using nano or your favorite editor:

```bash

nano /var/www/raschadvisory.com/html/index.html
#Paste html code
```

In order for Nginx to serve this content, it's necessary to create a server block with the correct directives. Instead of modifying the default configuration file directly, let’s make a new one at /etc/nginx/sites-available/example.com:

```bash

sudo nano /etc/nginx/sites-available/raschadvisory.com

```

Paste in the following configuration block, which is similar to the default, but updated for our new directory and domain name:

/etc/nginx/sites-available/example.com:

```bash
server {
        listen 80;
        listen [::]:80;

        root /var/www/raschadvisory.com/html;
        index index.html index.htm index.nginx-debian.html;

        server_name raschadvisory.com www.raschadvisory.com;

        location / {
                try_files $uri $uri/ =404;
        }
}
```



Next, let's enable the file by creating a link from it to the sites-enabled directory, which Nginx reads from during startup:

```bash

sudo ln -s /etc/nginx/sites-available/raschadvisory.com /etc/nginx/sites-enabled/
```



Next, test to make sure that there are no syntax errors in any of your Nginx files:

```bash

sudo nginx -t
```

### Fix
To avoid a possible hash bucket memory problem that can arise from adding additional server names, it is necessary to adjust a single value in the /etc/nginx/nginx.conf file. Open the file:

sudo nano /etc/nginx/nginx.conf
Find the server_names_hash_bucket_size directive and remove the # symbol to uncomment the line:

/etc/nginx/nginx.conf
...
http {
    ...
    server_names_hash_bucket_size 64;
    ...
}
...


If there aren't any problems, restart Nginx to enable your changes:


```bash

sudo systemctl restart nginx

```

Nginx should now be serving your domain name. You can test this by navigating to http://example.com, where you should see something like this:

Two server blocks are now enabled and configured to respond to requests based on their listen and server_name directives.

* example.com: Will respond to requests for example.com and www.example.com.
* default: Will respond to any requests on port 80 that do not match the other two blocks.

### NGINX Commands
Following are the important commands for NGINX.

- Start NGINX Web Server: sudo systemctl start nginx
- Stop NGINX Web Server: sudo systemctl stop nginx
- Restart NGNIX Web Server (stop and then start): sudo systemctl restart nginx
- Apply new NGINX Web Server configurations: sudo systemctl reload nginx
- By default NGINX start automatically. You can disable it with command: sudo systemctl disable nginx
Enable NGINX start up at boot: sudo systemctl enable nginx
Finally, NGINX Status: systemctl status nginx


### Important NGINX files and directories
NGINX Content: You can find the default NGINX HTML page at /var/www/html.
NGINX Server Configuration: All NGINX Configurations files are available at /etc/nginx

* conf.d  
* fastcgi.conf  
fastcgi_params  
koi-utf  
koi-win  
mime.types  
modules-available  
modules-enabled  
nginx.conf : The main NGINX configuration file. We can modify it later as per our requirement.
proxy_params  
scgi_params  
sites-available: We can find all the domain-specific configuration file in this directory. NGINX ignore the domain configuration if it not available in the sites-enabled directory.
sites-enabled: It contains links to configuration file available in sites-available directory files. We can find links for only active sites. In other words, if links for any particular config file is available it means that particular site is enabled and active.
snippets  
uwsgi_params  
win-utf
NGINX Server Logs

/var/log/nginx/access.log: Every request to our web server is recorded in this log file.
/var/log/nginx/error.log: All the NGINX errors are recorded in this log file.


### Important Nginx Files and Directories

Content
/var/www/html: The actual web content, which by default only consists of the default Nginx page you saw earlier, is served out of the /var/www/html directory. This can be changed by altering Nginx configuration files.
Server Configuration
/etc/nginx: The Nginx configuration directory. All of the Nginx configuration files reside here.
/etc/nginx/nginx.conf: The main Nginx configuration file. This can be modified to make changes to the Nginx global configuration.
/etc/nginx/sites-available/: The directory where per-site server blocks can be stored. Nginx will not use the configuration files found in this directory unless they are linked to the sites-enabled directory. Typically, all server block configuration is done in this directory, and then enabled by linking to the other directory.
/etc/nginx/sites-enabled/: The directory where enabled per-site server blocks are stored. Typically, these are created by linking to configuration files found in the sites-available directory.
/etc/nginx/snippets: This directory contains configuration fragments that can be included elsewhere in the Nginx configuration. Potentially repeatable configuration segments are good candidates for refactoring into snippets.
Server Logs
/var/log/nginx/access.log: Every request to your web server is recorded in this log file unless Nginx is configured to do otherwise.
/var/log/nginx/error.log: Any Nginx errors will be recorded in this log.




##Install PHP

Source: https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-ubuntu-18-04

sudo add-apt-repository universe





#################
Create an NGINX configuration in /etc/nginx/conf.d/ called rstudio.conf with the following configuration. Replace example.com with the public IP address or FDQN of your Linode:

/etc/nginx/conf.d/rstudio.conf



server {
        listen 80;
        listen [::]:80;

        server_name example.com;

        location / {
             proxy_pass http://localhost:8787/;
             proxy_redirect http://localhost:8787/ $scheme://$host/;
             proxy_http_version 1.1;
             proxy_set_header Upgrade $http_upgrade;
             proxy_set_header Connection $connection_upgrade;
             proxy_read_timeout 20d;
        }
}
##########################################


You can set-up access to the RStudio server via a proxy. By doing that and setting up the Apache or Nginx web server to use SSL, you will have secure access to the RStudio server.

Here's an example of how you can both Shiny and RStudio running on the same domain using SSL and Nginx. If you use https://YOURDOMAIN/ it will run your shiny apps; https://YOURDOMAIN/rstudio to be able to edit the shiny apps directly from the browser!

Replace YOURDOMAIN with your server URL:

map $http_upgrade $connection_upgrade {
 default upgrade;
 ''     close;
}

#Server with proxy
server {
 listen 443 ssl default_server;
 listen [::]:443 ssl default_server;
 ssl_certificate /etc/letsencrypt/live/YOURDOMAIN/cert.pem;
 ssl_certificate_key /etc/letsencrypt/live/YOURDOMAIN/privkey.pem;

 server_name YOURDOMAIN;

 location / {
     proxy_pass http://localhost:3838;
     proxy_redirect http://localhost:3838/ $scheme://$host/;
     proxy_http_version 1.1;
     proxy_set_header Upgrade $http_upgrade;
     proxy_set_header Connection $connection_upgrade;
     proxy_read_timeout 20d;
 }

 location /rstudio/ {
     rewrite ^/rstudio/(.*)$ /$1 break;
     proxy_pass http://localhost:8787;
     proxy_redirect http://localhost:8787/ $scheme://$host/rstudio/;
     proxy_http_version 1.1;
     proxy_set_header Upgrade $http_upgrade;
     proxy_set_header Connection $connection_upgrade;
     proxy_read_timeout 20d;
 }
}




## Create the SSL Certificate

SSL/TLS rely on a combination of public and private keys. While the private key portion of the SSL/TLS certificate is kept on the server, the public key is shared with all clients requesting information from your Ubuntu 18.04 server.

The private key encrypts data before it is sent to the client hence ensuring the security while the public key decrypts information from the server

So we need to create a self-signed private key and a certificate key pair. By default, Ubuntu 18.04 comes with OpenSSL – an open source implementation of the SSL and TLS protocol.

You can check the OpenSSL version number by typing the command below:

```bash
openssl version
```

```
## OpenSSL 1.1.0g  2 Nov 2017
```


Output


Creating the certificate and private key pair
We can create the certificate and private key pair using OpenSSL with just a single command listed below:

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/my.key -out /etc/ssl/certs/my.crt
```


You will be prompted to enter information that will be incorporated on your certificate request as show below:
```
Country Name:  e.g. KE
State or Province: e.g. CENTRAL
Locality Name:  Name of City e.g. NAIROBI
Organisation Name: e.g. MY SAMPLE COMPANY
Organizational Unit Name (eg, section) []: e.g. IT DEPARTMENT
Common Name (e.g. server FQDN or YOUR name) []: The exact domain name or public IP address e.g. www.example.com
Email Address: e.g. info@example.com

```
After answering the questions above, the private and crt files will be placed on the path that you specified on the OpenSSL command. For instance, in our case, the private key will be placed in /etc/ssl/private/my.key while the CRT will be placed in /etc/ssl/certs/my.crt






## Make pretty URLs for RStudio Server and Shiny Server

Source: https://www.r-craft.org/r-news/how-to-get-your-very-own-rstudio-server-and-shiny-server-with-digitalocean/
This is optional and a little more advanced. You might have noticed that to access both RStudio and Shiny Server, you have to remember weird port numbers (:8787 and :3838). Not only is it hard and ugly to remember, but some workplace environments often block access to those ports, which means that many people/places won’t be able to access these pages. The solution is to use a reverse proxy, so that nginx will listen on port 80 (default HTTP port) at the URL /shiny and will internally redirect that to port 3838. Same for RStudio - we can have nginx listen at /rstudio and redirect it to port 8787. This is why my Shiny apps can be reached at daattali.com/shiny/ which is an easy URL to type.

You need to edit the nginx config file /etc/nginx/sites-enabled/default:
```
sudo nano /etc/nginx/sites-enabled/default
```

Add the following lines right after the line that reads server_name _;

```
location /shiny/ {
  proxy_pass http://127.0.0.1:3838/;
}

location /rstudio/ {
  proxy_pass http://127.0.0.1:8787/;
}
```


Since we changed the nginx config, we need to restart nginx for it to take effect.



```bash
sudo service nginx restart
```


Now you should be able to go to http://123.456.1.2/shiny/ or http://123.456.1.2/rstudio/. Much better!

Bonus for advanced users: The above setup should be just fine for most users, but I did notice a few small issues with RStudio that seem to be fixed by allowing nginx to proxy WebSockets. For example, I noticed that when using the ggvis package in my RStudio, tooltips were not working. The fix is to add the following three lines inside the location /rstudio/ settings (keep the proxy_pass line and just add these three, and remember you have to restart nginx after changing the settings):
```
proxy_http_version 1.1;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection "upgrade";
```
If you’re hosting a Shiny Server, add these 3 lines after the proxy_pass line inside location /shiny/ as well.

Make your Shiny apps work with and without trailing slashes: If you have a Shiny app called “myapp”, then you would have to go to the URL http://123.456.1.2/shiny/myapp/ to see it. But if you omit the trailing slash (http://123.456.1.2/shiny/myapp), it will not work. I figured out a way to solve this, but again, keep in mind that I’m an nginx noob so it might not be a good solution. I added the following line inside location /shiny/ (just after the previous 3 lines from the previous paragraph):
```
rewrite ^(/shiny/[^/]+)$ $1/ permanent;
```
