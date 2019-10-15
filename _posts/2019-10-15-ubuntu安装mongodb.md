---
layout: post
title: 'Ubuntu18.04安装Mongodb'
date: 2019-10-15
author: sunjialei
tags:  ubuntu
---

安装步骤如下:

```css
ubuntu@VM-0-3-ubuntu:~$ wget https://repo.mongodb.org/apt/ubuntu/dists/bionic/mongodb-org/4.0/multiverse/binary-amd64/mongodb-org-server_4.0.10_amd64.deb

ubuntu@VM-0-3-ubuntu:~$ ar -vx mongodb-org-server_4.0.10_amd64.deb
```
后生成如下三个文件：x - debian-binary x - control.tar.xz x - data.tar.xz

```css
ubuntu@VM-0-3-ubuntu:~$ sudo mkdir /usr/local/mongodb
ubuntu@VM-0-3-ubuntu:~$ sudo cp data.tar.xz /usr/local/mongodb/
ubuntu@VM-0-3-ubuntu:/usr/local/mongodb$ sudo xz -d data.tar.xz (会变为一个data.tar压缩包)
ubuntu@VM-0-3-ubuntu:/usr/local/mongodb$ sudo tar -xvf data.tar

ubuntu@VM-0-3-ubuntu:/usr/local/mongodb$ sudo apt install mongodb-server-core 
ubuntu@VM-0-3-ubuntu:/usr/local/mongodb$ sudo apt install mongodb-clients
ubuntu@VM-0-3-ubuntu:/usr/local/mongodb$ sudo mkdir data
ubuntu@VM-0-3-ubuntu:/usr/local/mongodb$ sudo mkdir logs
```

配置文件
```css
ubuntu@VM-0-3-ubuntu:/usr/local/mongodb$ sudo vim mongod.conf
```

填写配置
```css
dbpath=/usr/local/mongodb/data
logpath=/usr/local/mongodb/logs/mongod.log
logappend=true
fork=true
port=27017
bind_ip=0.0.0.0
# 需要认证
#auth=true
```

后台启动
```css
ubuntu@VM-0-3-ubuntu:/usr/local/mongodb$ sudo usr/bin/mongod -f mongod.conf
```

设置用户密码
```css
use admin
db.createUser({user:"root", pwd:"password*", roles:[{role:'root', 'db': 'admin'}], mechanisms: ["SCRAM-SHA-1"]})
配置文件开启认证：auth=true
重启mongodb
```

验证用户密码
```css
use admin
db.auth('root', 'password')

use blog
db.createUser({user:"blog", pwd:"xxx", roles:[{role:'dbOwner', 'db': 'blog'}], mechanisms: ["SCRAM-SHA-1"]})
```

接下来可以用可视化工具来连接mongodb了


