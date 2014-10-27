---
layout: post
title: Nginx config PHP
---

![Miia](http://ww4.sinaimg.cn/mw1024/6dc1b103gw1ewb662ga0bj20i20b4t9y.jpg)

Nginx PHP vhost config.<!-- more -->下面是一段取至[homestead](https://github.com/laravel/homestead/blob/master/scripts/serve.sh){:target="_blank"}的shell脚本,可以帮助我们快速的配置vhost.

    #!/usr/bin/env bash

    block="server {
        listen ${3:-80};
        server_name www.$1;
        return 301 http://$1\$request_uri;
    }

    server {
        listen ${3:-80};
        server_name $1;
        root \"$2\";

        index index.html index.htm index.php;

        charset utf-8;

        location / {
            try_files \$uri \$uri/ /index.php?\$query_string;
        }

        location = /favicon.ico { access_log off; log_not_found off; }
        location = /robots.txt  { access_log off; log_not_found off; }

        access_log off;
        error_log  /var/log/nginx/$1-error.log error;

        sendfile off;

        client_max_body_size 100m;

        location ~ \.php$ {
            fastcgi_split_path_info ^(.+\.php)(/.+)$;
            fastcgi_pass unix:/var/run/php5-fpm.sock;
            fastcgi_index index.php;
            include fastcgi_params;
            fastcgi_param SCRIPT_FILENAME \$document_root\$fastcgi_script_name;
            fastcgi_intercept_errors off;
            fastcgi_buffer_size 16k;
            fastcgi_buffers 4 16k;
            fastcgi_connect_timeout 300;
            fastcgi_send_timeout 300;
            fastcgi_read_timeout 300;
        }

        location ~ /\.ht {
            deny all;
        }
    }
    "

    echo "$block" > "/etc/nginx/sites-available/$1"
    ln -fs "/etc/nginx/sites-available/$1" "/etc/nginx/sites-enabled/$1"
    service nginx reload

Shell 下载地址:[请戳我](https://gist.githubusercontent.com/poem/05c1977a7331a360a880/raw/e026c73b62b0d390b8fb88e0c2cfc26b003ab745/serve.sh){:target="_blank"}

该 shell 脚本有三个参数,$1 一般是网站域名,$2 是网站代码根目录路径,$3 是访问端口,默认为80.然后只需要运行

    sudo sh serve.sh blog.jjyy.me /var/www/blog.jjyy.me
