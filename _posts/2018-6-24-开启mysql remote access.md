---
layout: post
title: '允许远程访问mysql,开启remote access'
date: 2018-6-24
author: sunjialei
tags:  linux
---

比如在多人开发的情况下,需要使用同一台服务器的数据库,每个开发人员本地使用如Navicat这类的mysql管理工具远程连接这台服务器,可能无法连接上,这个时候就需要开启mysql remote access。步骤如下：

1.进入服务器mysql配置文件中

```linux
cd /etc/mysql/mysql.conf.d

sudo vim mysqld.cnf
```

其中有一行: bind-address = 127.0.0.1,这相当于白名单,只有ip地址在里面的才能访问这台服务器的mysql数据库,只要把这行注释掉即可

```linux
#bind-address =  127.0.0.1
```

2.对mysql的默认用户进行主机设置

```linux
cd /etc/mysql

mysql -u root -p

mysql>use mysql;

mysql>update user set host = '%' where user = 'root';

mysql>exit
```

3.重启mysql,我的服务器是Ubuntu
```linux
sudo service mysql restart
```

这样就可以远程使用图形界面管理工具连接mysql了
