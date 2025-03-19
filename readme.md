# Setup

1. Install brew
2. Install php
3. Install nginx

- Add project to nginx servers/
- Create new file in /opt/homebrew/etc/nginx/servers/

```
server {
    listen 80;
    server_name localhost;
    
    root /usr/local/var/www;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    # PHP processing
    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass 127.0.0.1:9000; # PHP-FPM listens on port 9000
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    error_page 404 /404.html;
}
```