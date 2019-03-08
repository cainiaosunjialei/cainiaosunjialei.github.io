---
layout: post
title: 'JS深拷贝与浅拷贝'
date: 2019-3-8
author: sunjialei
tags:  Javascript
---

JS中数据类型有两大类：

    简单数据类型：number,string,bool,null,undefined,symbol

    复杂数据类型：object,function,array

只有复杂数据类型才有深拷贝浅拷贝的说法。

```javascript
let a = 1
let b = a
b = 2

console.log(a) //1
console.log(b) //2
```
简单数据类型把变量a赋值给了变量b,其实是在栈内存中重新开辟了一块空间用来存储变量b以及b的值。a和b所在的两块栈内存是互不影响的,修改b的值并不会影响a的值。


```javascript
let a = {
    name: '张三',
    age: 18
}
let b = a
b.name = '李四'

console.log(a) //{name: "李四", age: 18}
console.log(b) //{name: "李四", age: 18}
```
复杂数据类型栈内存中存放的是变量名a以及变量a的值的引用,这个引用指向堆内存,堆内存中存储的才是变量a的值,栈内存中存的是变量a的值的引用。把变量a赋值给了变量b,其实是在栈内存中把变量a的引用给了变量b,此时变量a和变量b的引用都指向同一个堆内存。改变其中一个的值另外个的值也会跟着改变。这其实就是浅拷贝

### 浅拷贝就是各自的引用都指向同一块堆内存,相互影响。深拷贝就是各自的引用指向各自的堆内存,双方互不影响

### 如何实现深拷贝？
1.通过Json对象stringify和parse
```javascript
let a = {
    name: '张三',
    age: 18
}
let b = JSON.parse(JSON.stringify(a))
b.name = '李四'

console.log(a) //{name: "张三", age: 18}
console.log(b) //{name: "李四", age: 18}
```

2.ES6的Object.assign()
```javascript
let a = {
    name: '张三',
    age: 18
}
let b = Object.assign({}, a)
b.name = '李四'

console.log(a) //{name: "张三", age: 18}
console.log(b) //{name: "李四", age: 18}
```

3.递归(下面的一段代码我是从掘金社区别人那拿过来的)
```javascript
function deepCopy(obj) {
    // 创建一个新对象
    let result = {}
    let keys = Object.keys(obj),
        key = null,
        temp = null;

    for (let i = 0; i < keys.length; i++) {
        key = keys[i];    
        temp = obj[key];
        // 如果字段的值也是一个对象则递归操作
        if (temp && typeof temp === 'object') {
            result[key] = deepCopy(temp);
        } else {
        // 否则直接赋值给新对象
            result[key] = temp;
        }
    }
    return result;
}

var obj1 = {
    x: {
        m: 1
    },
    y: undefined,
    z: function add(z1, z2) {
        return z1 + z2
    },
    a: Symbol("foo")
};

var obj2 = deepCopy(obj1);
obj2.x.m = 2;

console.log(obj1); //{x: {m: 1}, y: undefined, z: ƒ, a: Symbol(foo)}
console.log(obj2); //{x: {m: 2}, y: undefined, z: ƒ, a: Symbol(foo)}
```

### 注意：Object.assign()对于源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用，看下面
```javascript
let a = {
    name: '张三',
    foo: {
        x: 1
    }
}
let b = Object.assign({}, a)
b.name = '李四'
b.foo.x = 2

console.log(a) //{name: "张三", foo: {x: 2}}
console.log(b) //{name: "李四", foo: {x: 2}}
```
所以Object.assign()对于一维对象是深拷贝,对于二维对象是浅拷贝








