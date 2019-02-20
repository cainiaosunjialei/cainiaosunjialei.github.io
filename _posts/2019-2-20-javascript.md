---
layout: post
title: 'JavaScript之作用域链与闭包'
date: 2019-2-20
author: sunjialei
tags:  Javascript
---

什么是闭包? 《JavaScript高级程序设计(第3版)》中这么定义闭包：闭包是有权访问另一个函数作用域中的变量的函数。

闭包一般会涉及到作用域链的问题，所以我们也得搞清楚啥是作用域链
```javascript
var color = "blue";
function changeColor() {
    var anotherColor = "red";
    function swapColors() {
        var tempColor = anotherColor;
        anotherColor = color;
        color = tempColor;

        // 这里可以访问 color、anotherColor 和 tempColor 
    }
    // 这里可以访问 color 和 anotherColor，但不能访问 tempColor 
    swapColors();
}
// 这里只能访问 color 
changeColor();
```
这里有三个作用域,最外层的全局作用域,函数changeColor的作用域,函数swapColors的作用域。这三个作用域会形成一条作用域链,内层的作用域能访问外层作用域中的变量，但外层作用域无法访问内层作用域中的变量。所以对于swapColors函数来说,它能访问到外层函数changeColor中的变量以及再外层作用域也就是全局作用域中的变量color。changeColor函数无法访问swapColors函数中的变量，但changeColor可以访问它自己外层的作用域中的变量及能访问到color变量。

再来看下闭包的定义：闭包是有权访问另一个函数作用域中的变量的函数。

首先闭包得是个函数,它能访问到另外一个函数作用域中的变量。所以在上面这段代码中swapColors就是一个闭包。因为swapColors函数它能访问到changeColor函数中的变量anotherColor。

也可以把闭包理解为：定义在一个函数内部的函数

看下面2段代码:
```javascript
var a = [];
for (let i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 6
```

```javascript
var a = [];
for (var i = 0; i < 10; i++) {
  a[i] = function () {
    console.log(i);
  };
}
a[6](); // 10
```
let是ES6中出现的,let的出现使得原本没有块级作用域的javascript有了块级作用域。因为let的出现我觉得闭包的定义需要改一下，改成下面这段话：

闭包是有权访问另一个函数作用域或块级作用域中的变量的函数。

第一段代码,由于let的存在for循环变成了一个块级作用域,function() {console.log(i)} 形成了一个闭包,去找它的外层的变量i,保存了当时循环时的变量i的值,所以值是6

第二段代码，在ES6之前还没有let的时候,javascript中还不存在块级作用域。function() {console.log(i)}不是闭包,不会保存当时循环的时候的变量i的值,只有在调用
```javascript  
a[6]()
```
的时候才会去取值,在调用之前循环已经结束,此时变量i的值为10且存在于全局作用域中。function() {console.log(i)}会沿着作用域链寻找变量i,function() {console.log(i)}的上级作用域就是全局作用域,所以i的值会是10

如果不用let怎么样让输出的值为6呢？立即执行函数就可以
```javascript  
var a = [];
for (var i = 0; i < 10; i++) {
    (function(num){
        a[i] = function () {
            console.log(num);
        };
    })(i)
}
a[6](); // 6
```
这里又形成了一个闭包,所以每次循环的时候的值会被保存下来。










