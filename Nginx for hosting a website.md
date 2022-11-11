# Nginx
## Install Nginx on Ubuntu 22.04
```sudo apt install nginx```
## Nginx basic command
Changes made in the configuration file will not be applied until the command to reload configuration is sent to nginx or it is restarted. To reload configuration, use below command:
```nginx -s reload``` 

## Remove Nginx completely (including config files)
```sudo apt purge nginx nginx-common```

## Remove Nginx but keep config files
```sudo apt remove nginx```

## Config files needed to edit
```/etc/nginx/nginx.config```
```/etc/nginx/sites-available/default```

### /etc/nginx/sites-available/default
```
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
```

### /etc/nginx/nginx.conf
```
user  www-data www-data;
worker_processes  1;
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;
events {
    worker_connections  1024;
}
http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;
    log_format  main  \'$remote_addr - $remote_user [$time_local] \"$request\" \'
                      \'$status $body_bytes_sent \"$http_referer\" \'
                      \'\"$http_user_agent\" \"$http_x_forwarded_for\"\';
    access_log  /var/log/nginx/access.log  main;
    sendfile        on;
    #tcp_nopush     on;
    keepalive_timeout  65;
    gzip  on;
    gzip_disable \"msie6\";
  include /etc/nginx/conf.d/*.conf;
  include /etc/nginx/sites-enabled/*.conf;
}
```
## Enable fire wall for specific port
```sudo ufw allow 443``` (allow specific port come through fire wall)
```sudo ufw status``` (check fire wall status)```
