---
layout: post
title: 'CSS定位position'
date: 2019-2-3
author: sunjialei
tags:  CSS
---

最近在学习原生JavaScript,有个练手的小demo,放大镜的功能。做的过程中遇到一些跟CSS定位有关的知识,已经忘记了，只能回头重新学习下CSS的position知识点。

CSS的position属性有4种值：static,relative,absolute,fixed
### 1.static
默认的定位方式,不设置position属性默认就是static定位
```html
<!DOCTYPE html>
<html>
<head>
    <style>
        body {
            background-color: gray
        }
        #orange {
            width: 300px;
            height: 300px;
            background-color: orange;
        }
        #box {
            width: 150px;
            height: 150px;
            background-color: yellow;
        }
    </style>
</head>
<body>
    <div id="orange"></div>
    <div id="box"></div>
</body>
</html>
```
<img class="header-img" src="/assets/img/2019-2-3-1.png" alt="">

### 2.relative 相对定位
relative相对于它自身默认情况下的位置进行定位。什么意思呢?看下面

给box加上相对定位
```html
<!DOCTYPE html>
<html>
<head>
    <style>
        body {
            background-color: gray
        }
        #orange {
            width: 300px;
            height: 300px;
            background-color: orange;
        }
        #box {
            width: 150px;
            height: 150px;
            background-color: yellow;
            position: relative;
            left: 50px;
            top: 50px
        }
    </style>
</head>
<body>
    <div id="orange"></div>
    <div id="box"></div>
</body>
</html>
```
<img class="header-img" src="/assets/img/2019-2-3-2.png" alt="">
box相对于它原来的位置left了50px,top了50px。原来的位置是没有设置position:relative时的box


### 3.absolute 绝对定位
absoulute是相对于它的父元素,注意:是有定位的父元素来说的,排除父元素为position:static这种情况,如果父元素都没有定位，那么就是相对于body来定位。如下：

1.父元素没有定位的情况
```html
<!DOCTYPE html>
<html>
<head>
    <style>
        body {
            background-color: gray;
        }
        #orange {
            width: 300px;
            height: 300px;
            background-color: orange;
            margin-left: 200px;
            margin-top: 200px;
        }
        #box {
            width: 150px;
            height: 150px;
            background-color: yellow;
            position: absolute;
            left: 50px;
            top: 50px
        }
    </style>
</head>
<body>
    <div id="orange">
        <div id="box"></div>
    </div>
</body>
</html>
```
box的父元素是orange,父元素没有定位,继续冒泡往上找,上面没有父元素了,就找body，这时候的box的定位是相对于body来定位的
<img class="header-img" src="/assets/img/2019-2-3-3.png" alt="">


2.父元素有定位的情况
```html
<!DOCTYPE html>
<html>
<head>
    <style>
        body {
            background-color: gray;
        }
        #orange {
            width: 300px;
            height: 300px;
            background-color: orange;
            margin-left: 200px;
            margin-top: 200px;
            position: relative
        }
        #box {
            width: 150px;
            height: 150px;
            background-color: yellow;
            position: absolute;
            left: 50px;
            top: 50px
        }
    </style>
</head>
<body>
    <div id="orange">
        <div id="box"></div>
    </div>
</body>
</html>
```
box的父元素是orange有定位,这时候的box的定位是相对于orange来定位的
<img class="header-img" src="/assets/img/2019-2-3-4.png" alt="">

### 4.fixed 固定定位
fixed固定定位相对于浏览器窗口定位,不论滚动条拉动与否,不论其父元素是否设置定位,位置始终不变










