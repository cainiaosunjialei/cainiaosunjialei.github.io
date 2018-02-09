---
layout: post
title: 'php中神奇的转义'
date: 2018-2-10 
author: sunjialei
tags:  php
---

今天发现个奇怪的事。如下

\ \在双引号中会转义成 \
```php
<?php
	echo "\\";
```

结果：
```php
	\
```

## 但是,\ \在单引号中竟然也会转义成 \
```php
<?php
	echo '\\';
```
结果：
```php
	\
```

真是太神奇了。我查了下，发现 \ '在单引号中也会转义,但在双引号中不存在转义的情况
```php
<?php
	echo '\'';
	echo "<br>";
	echo "\'";
```
结果：
```php
	'
	\'
```