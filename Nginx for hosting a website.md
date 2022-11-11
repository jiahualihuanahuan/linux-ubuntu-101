# Nginx
## Install Nginx on Ubuntu 22.04
sudo apt install nginx

## Remove Nginx completely (including config files)
sudo apt purge nginx nginx-common

## Remove Nginx but keep config files
sudo apt remove nginx

## Config files needed to edit
/etc/nginx/nginx.config
/etc/nginx/sites-available/default

### /etc/nginx/sites-available/default
server {
    listen              80; (listen for port 80 which is the unsecured http)
    listen              443 ssl; (listen for port 443 which is the secured https)
    server_name         www.example.com;
    ssl_certificate     www.example.com.crt;
    ssl_certificate_key www.example.com.key;
    ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers         HIGH:!aNULL:!MD5;
    ...
    root /var/www/html (path to your website files)
}

### /etc/nginx/nginx.conf
