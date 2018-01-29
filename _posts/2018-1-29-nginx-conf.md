---
layout: post
title: 'Linux下配置Nginx'
date: 2018-1-29
author: sunjialei
tags:  nginx linux
---

Linux下Nginx的简单配置

### 1.进入到安装Nginx的目录
```nginx
	cd /usr/local/nginx
```

### 2.进入nginx的配置文件nginx.conf
```nginx
	vim nginx.conf
```

### 3.在nginx目录下创建一个conf.d文件夹,在配置文件中将该文件夹下的文件引入
```nginx
	include /usr/local/nginx/conf.d/*.conf
```

### 4.在conf.d文件夹下创建文件如live.conf,进入live.conf目录
```nginx
	server {
        listen  8001;
        server_name  example1.com;

        location / {
            root   /data/live/trunk/system/backend/web;
            index  index.php index.html index.htm;
            try_files $uri $uri/ /index.php?$args;
        }

        location ~ .php$ {
            fastcgi_pass   127.0.0.1:9000;
            fastcgi_index  index.php;
            fastcgi_param  SCRIPT_FILENAME  /data/live/trunk/system/backend/web$fastcgi_script_name;
            include        fastcgi_params;

        }
	}
	其中listen是端口号,server_name是网站域名,root指向的是网站的根目录

```

### 5.重启nginx服务器
进入nginx目录中,执行：
```nginx
	sbin/nginx -s reload
	
```


