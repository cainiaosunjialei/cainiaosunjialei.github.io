---
layout: post
title: 'CSS子div的margin-top属性不生效的解决办法'
date: 2019-10-15
author: sunjialei
tags:  CSS
---

#### 原因:如果父div元素没有垂直padding和boder，子元素的垂直margin就会与父元素叠加，也就是说，表现是子元素的垂直margin变成了父元素的，子元素与父元素之间没有了垂直margin。

#### 解决办法：
    1.给父元素添加padding-top,如padding-top:1px
    2.给父元素添加overflow:hidden

