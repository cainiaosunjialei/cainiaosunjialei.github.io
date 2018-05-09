---
layout: post
title: 'Windows下Phalcon的安装以及phpstorm识别phalcon语法及提示'
date: 2018-5-6 
author: sunjialei
tags:  php phalcon
---

新入职一家公司,使用的开发框架是Phalcon框架,下面是使用这个框架之前的一些准备工作。

1.由于Phalcon是C语言写的一个扩展,所以需要安装这个扩展php_phalcon.dll,下载地址https://github.com/phalcon/cphalcon/releases,
然后将这个扩展文件放在相对应的文件中,我这边存放的位置是C:\php\laragon\bin\php\php-7.1.12-Win32-VC14-x64\ext下,然后在php.ini文件中添加extension=php_phalcon.dll。重启服务器,查看扩展是否安装成功,如果成功的话会看到![这里写图片描述](https://img-blog.csdn.net/20180506232056247?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)代表扩展安装成功。

2.接下去要安装一个脚手架工具phalcon-devtools,下载地址https://github.com/phalcon/phalcon-devtools，将文件解压至www目录，设置环境变量，指向该目录
![这里写图片描述](https://img-blog.csdn.net/20180507224623508?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
接下来测试是否ok，打开cmd，运行phalcon，
![这里写图片描述](https://img-blog.csdn.net/20180507224746650?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)说明ok。

使用命令：
```php
phalcon create-project store
```
会生成框架,
![这里写图片描述](https://img-blog.csdn.net/20180507225853689?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70).

3.在phpstorm中自动生成controller和model，File/Settings/Tools/command Line Tool Support
![这里写图片描述](https://img-blog.csdn.net/20180507230601700?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
点右上的+号
![这里写图片描述](https://img-blog.csdn.net/20180507230901908?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
选择Custom tool,点击OK，
![这里写图片描述](https://img-blog.csdn.net/20180507231132363?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)Tool path为phalcon-devtools的目录，点击ok。重启phpstorm,这时候就可以自动生成controller和model了
命令：
```php
phalcon controller --name test     //自动生成TestController

phalcon model--name test		  //自动生成表名为test的model
```

4.但这个时候还有个问题，phpstorm没有phalcon的代码提示。
解决办法：打开phalcon-devtools文件下ide文件下的gen-stubs.php,修改第15行代码，修改为
```php
define('CPHALCON_DIR' , 'C:\php\laragon\www\phalcon-devtools-master');
```
第2个参数是你目录的位置。

 然后执行命令
```php
php gen-stubs.php
```
这时候会在ide文件下生产1个带版本名称的文件夹
![这里写图片描述](https://img-blog.csdn.net/20180507225536716?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
打开phpstorm，右键，
![这里写图片描述](https://img-blog.csdn.net/2018050723154828?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
然后
![这里写图片描述](https://img-blog.csdn.net/20180507231810676?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) 
选择Specify Other,然后选择ide下生成的版本号目录下Phalcon目录，点击OK，
![这里写图片描述](https://img-blog.csdn.net/20180507232024159?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3N1bl9qaWFsZWk=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
重启phpstorm，这个时候phpstorm能够识别phalcon的代码了




