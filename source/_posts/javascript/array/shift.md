---
title: shift()删除数组第一个元素
date: 2018-02-07 17:42:01
tags:
  - Javascript
  - JS数组
---


**概述**
shift()方法用于从当前数组中移除第一个元素，并返回被移除的元素。

**语法**

```
array.shift()
```

**返回值**
shift()方法的返回值为任意类型，返回被移除的元素。如果该数组为空，则不改变这个空数组，返回undefined。

本方法会移除数组中的第一个元素，数组的length属性也会随之减 1 (如果数组中有元素的话)。

**示例**

```
var arr = ['萤光之烛', 2018, true, 1234];

var result = arr.shift();
console.log(result);    // 萤光之烛
console.log(arr);       // [2018, true, 1234]

var emptArray = [];
var res = emptArray.shift();
console.log(res);       // undefined
```
```