---
title: pop()删除最后一个元素
date: 2018-02-04 17:13:11
tags:
  - Javascript
  - JS数组
---

**概述**
pop()方法用于从当前数组中移除最后一个元素，并返回被移除的元素。

**语法**

```
array.pop()
```

**返回值**
pop()方法的返回值为任意类型，返回被移除的元素。如果该数组为空，则不改变这个空数组，返回undefined。
本方法会移除数组中的最后一个元素，数组的length属性也会随之减 1 (如果数组中有元素的话)。

**示例**

```
var arr = ['萤光之烛', 2018, true, 1234]

var result = arr.pop();
console.log(result);    // 1234
console.log(arr);       // ["萤光之烛", 2018, true]

var emptArray = [];
var res = emptArray.pop();
console.log(res);       // undefined
```
```