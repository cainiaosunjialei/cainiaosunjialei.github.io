---
layout: post
title: 'JavaScript函数中的arguments'
date: 2019-2-11
author: sunjialei
tags:  Javascript
---

记录一下以前没注意的一个知识点

在JavaScript中给函数传递参数，函数是以数组的形式接收参数的，所以不管给函数传多少个参数，函数都是可以接受的。在函数中获取参数可以使用arguments对象以数组的形式获取。

```javascript
function add() {
    console.log(arguments[0])  //10
    console.log(arguments[1])  //20
}

add(10,20)
```

```javascript
function add() {
    console.log(arguments[0])  //10
    console.log(arguments[1])  //undefined
}

add(10)
```

```javascript
function add(num1, num2) {
    console.log(arguments[0])  //10
    console.log(num1)  //10
    console.log(arguments[1])  //20
    console.log(num2)  //20
}

add(10, 20)
```

```javascript
function add(num1, num2) {
    console.log(arguments[0])  //10
    arguments[1] = 30
    console.log(arguments[1])  //30
    console.log(num2)  //30
}

add(10, 20)
```

在严格模式下：
```javascript
"use strict"
function add(num1, num2) {
    console.log(arguments[0])  //10
    arguments[1] = 30
    console.log(arguments[1])  //30
    console.log(num2)  //20
}

add(10, 20)
```











