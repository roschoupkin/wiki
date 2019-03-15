# NGINX SETUP
*Here is a guide to configure `NGINX`, so that a specific port looks in the right folder (settings for the main tasks in the `frontend`)*

> **Note:** Imagine that you have a project in which the back and front (say) look at different ports

### 1. Connect to server
```
ssh user@host -p port
```

### 2. Go to the root directory of the server and create a folder in which  the port will looks
```
cd ~/var/www/
mkdir front // add index.html as needed
```

### 3. Go to the available sites and check if the default settings file exists. And make copy of default
```
cd ~/etc/nginx/sites-available
ls // Check, that we have default settings file
cp @default @new_file
```

### 4. Fill the file with the necessary settings (in our example for the front)
* Open file in editor
```
nano @new_file // mceditor and other we can use also
```

* Then we add follow code
```
server {
    error_log  /var/log/nginx/front.error.log  info;
    listen 8084;
    listen [::]:8084;
    client_max_body_size 128M;
    root /var/www/front;
    index index.html;
    server_name localhost;
    charset utf-8;

    gzip on;
    gzip_vary on;
    gzip_disable "msie6";
    gzip_comp_level 6;
    gzip_min_length 1100;
    gzip_buffers 16 8k;
    gzip_proxied any;
    gzip_types
        text/plain
        text/css
        text/js
        text/xml
        text/javascript
        application/javascript
        application/x-javascript
        application/json
        application/xml
        application/xml+rss;

    location / {
        try_files $uri /index.html;
    }

    location ~* \.(?:jpg|jpeg|gif|png|ico|cur|gz|svg|svgz|mp4|ogg|ogv|webm|htc|svg|woff|woff2|ttf)$ {
        expires 1M;
        access_log off;
        add_header Cache-Control "public";
    }

    location ~* \.(?:css|js)\$ {
        expires 7d;
        access_log off;
        add_header Cache-Control "public";
    }

    location ~ /\.ht {
        deny  all;
    }
}
```
> **Note:** `8084` - our port, `front` - our folder with project code

### 5. We need to create a link to the configuration file
```
cd ~/etc/nginx/sites-enabled
ln -l /etc/nginx/sites-available/front /etc/nginx/sites-enabled/front // Create a link
```

### 6. Check configuration for validity and reload server
```
nginx -t
service nginx reload // or nginx reload
```

> **Note:** If necessary, use **sudo** before commands (It's normal)
