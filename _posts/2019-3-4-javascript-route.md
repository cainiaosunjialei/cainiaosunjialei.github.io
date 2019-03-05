---
layout: post
title: '简述为什么在Vue中当路由模式为history的时候刷新页面会404'
date: 2019-3-5
author: sunjialei
tags:  Javascript
---
上周五遇到个问题,vue的路由为history模式,当在正式环境的时候刷新页面会出现404 Not Found的情况。于是查了相关资料算是搞明白了，顺便记录下。

vue-router的路由有2种模式：1.hash 2.history,

如：

hash模式：http://localhost:3000/#/user/123

history模式：http://localhost:3000/user/123

不管在浏览器中url输入的是什么，都会先根据这个url去请求服务器。为什么vue叫单页面，是因为请求服务器的时候不管请求的地址是什么,永远只返回同一个页面，默认index.html。但你可能会问url地址不是不同吗,为什么返回的页面都是同一个index.html。

hash模式请求服务器的时候#号和#号后面部分不会携带着，及hash模式下请求服务器的时候,请求的地址永远都是http://localhost:3000/,history模式下若后端不进行配置,在vue页面中通过按钮之类的跳转是没什么问题的，但刷新页面的时候会出现404,是因为浏览器通过url去请求后端的时候请求的地址是http://localhost:3000/user/123,但后端并没有这个路由,找不到对应的路由，所以报404,这个时候就需要后端进行相关配置,把请求指向http://localhost:3000/。这时候返回的页面又都是index.html了，index.html中加载了很多js文件,到这一步之后，前端路由就起作用了,vue-router会捕捉浏览器地址中的/user/123,然后找到这个前端路由,渲染相应的页面。









