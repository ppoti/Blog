---
title: unshift()添加元素
date: 2018-02-11 09:27:33
tags:
  - Javascript
  - JS数组
---


**概述**
unshift()方法用于向当前数组的开头位置添加一个或多个元素，并返回添加元素后数组长度

**语法**

```
array.unshift(element1, ..., elementN)
```

**参数**

```
element1	任意类型添加到当前数组开头位置的元素。
elementN	可选/任意类型要添加到当前数组末开头位置的其他项，可以有多个。

```

**返回值**

unshift()方法的返回值为Number类型，返回添加元素后数组的长度。

**示例**

```
var arr = ['萤光之烛', 2018];

var result = arr.unshift("www","com");
console.log(result);   // 4
console.log(arr);      // ['www', 'com', '萤光之烛', 2018]
```