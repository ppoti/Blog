---
title: isArray()是否为数组
date: 2018-02-18 15:31:01
tags:
  - Javascript
  - JS数组
---


**概述**
Array.isArray()方法用来判断某个值是否为数组。如果是，返回 true，否则返回 false。

**语法**

```
Array.isArray(value)
```

**参数**

```
value	任意类型需要被检测的值。

```


**返回值**

Array.isArray()方法的返回值为Boolean类型，被检测的值为数组返回 true，不是数组返回 false。

**示例**

```
// 下面的函数调用都返回 true
Array.isArray([]);
Array.isArray([1]);
Array.isArray(new Array());

// 鲜为人知的事实：其实 Array.prototype 也是一个数组。
Array.isArray(Array.prototype); 

// 下面的函数调用都返回 false
Array.isArray();
Array.isArray({});
Array.isArray(null);
Array.isArray(undefined);
Array.isArray(17);
Array.isArray('Array');
Array.isArray(true);
Array.isArray(false);
Array.isArray({ __proto__: Array.prototype });
```

兼容

```
把下面的代码插入到脚本的开头来解决低级IE的兼容。
if (!Array.isArray) {
  Array.isArray = function(arg) {
    return Object.prototype.toString.call(arg) === '[object Array]';
  };
}
```