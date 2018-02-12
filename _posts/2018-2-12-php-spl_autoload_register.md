---
layout: post
title: '关于php的命名空间非限定、限定、完全限定的理解与自动加载之spl_autoload_register()'
date: 2018-2-12 
author: sunjialei
tags:  php
---

做项目这么久以来一直没有好好的静下心来对自身思考有哪些不足之处,有些东西虽然用了，但没去考虑过为什么是这样的，现在越来越觉得自己基础不够扎实。虽然我不是科班出身也没有在培训班培训过,但干这行就得靠自己去悟去想。

最近思考了以下2个问题：

#### 1.为什么有时候实例化一个类是以\开头的,有的时候又不是呢?

#### 2.为什么在Yii 2、 Laravel 5这类的框架控制器中new一个对象,框架能知道获取的是哪个路径下的文件呢？

针对于上面2个问题,我解答下。

我在我本地C:\php\laragon\www目录下新建一个文件夹名为test
然后建立以下结构
<img class="header-img" src="/assets/img/2018-2-12.png" alt="">

Autoloader.php
```php
<?php
	namespace test;

	spl_autoload_register(function($className) {
		$className = str_replace('\\', DIRECTORY_SEPARATOR, $className);
		$path = dirname(__DIR__);
		$fullFile = $path . DIRECTORY_SEPARATOR .$className.'.php';
		if (file_exists($fullFile)) {
			include  $fullFile;
		} else {
			echo '文件'.$fullFile.'不存在';
		}
	});
```

MyTool.php
```php
<?php
	namespace test\src\tools;

	class MyTool {

		public function __construct() {
			echo 'mytool';
		}
	}	
```



index.php
```php
<?php
	namespace test;

	include 'Autoloader.php';

	class A {

		public function __construct () {
			echo '怎么能';
		}
	}

	$res = new A(); 
	echo "<br>";

	$res = new src\tools\MyTool();
	echo "<br>";

	$res = new \test\src\tools\MyTool();
	echo "<br>";

	$res = new \src\tools\MyTool(); 
```
运行结果：
```php
	怎么能

	mytool

	mytool

	文件C:\php\laragon\www\src\tools\MyTool.php不存在
Fatal error: Uncaught Error: Class 'src\tools\MyTool' not found in C:\php\laragon\www\test\index.php:22 Stack trace: #0 {main} thrown in C:\php\laragon\www\test\index.php on line 22
```

#### 原因：

#### 由于当前index.php命名空间为test,new A()代表在test命名空间中寻找类名为A的类然后实例化。这种方式为非限定名称

#### 由于当前index.php命名空间为test,new src\tools\MyTool()代表在命名空间为test\src\tools下寻找类名为MyTool的类然后实例化。这种方式称为限定名称

#### new \test\src\tools\MyTool(),这个前面有\,这种方式称为完全限定名称,不管当前命名空间是啥,寻找命名空间为test\src\tools下类名为MyTool的类然后实例化

#### new \src\tools\MyTool(), 同上,由于不存在命名空间为src\tools下的MyTool的类,所以报错

那么又有个问题,它是怎么寻找文件路径的呢?在index.php中引入Autoloader.php这个文件,当new src\tools\MyTool()的时候在去调用spl_autoload_register这个方法,传入的className是 test\src\tools\MyTool,最终找的文件名称路径为C:\php\laragon\www\test\src\tools\MyTool.php，如果存在该文件则导入该文件。如果在顶部使用了use test\src\tools,new MyTool(),传入的className还是test\src\tools\MyTool。

Laravel、Yii这类框架中都在入口文件中使用了spl_autoload_register这个方法进行自动加载



