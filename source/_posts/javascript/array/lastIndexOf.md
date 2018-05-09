---
title: lastIndexOf()查找元素最后一次的索引
date: 2018-02-15 10:17:53
tags:
  - Javascript
  - JS数组
---

**概述**
lastIndexOf()方法用于查找给定元素在当前数组中最后一次出现的位置。

**语法**

```
array.lastIndexOf(searchElement, fromIndex)
```

**参数**

```
searchElement	任意类型要在数组中查找的元素。
fromIndex	可选/Number类型 指定从数组中开始查找的索引位置。

```

注意： 
lastIndexOf()方法将从后向前查找给定元素，并返回给定元素第一次出现的位置。因为是从后向前搜索，第一次出现的位置就是该元素在当前数组中最后一次出现的位置。

如果不指定 fromIndex 值，则从最后一个元素开始搜索整个数组。
如果 fromIndex 的值大于数组长度，则意味查找整个数组，从最后一个元素开始搜索整个数组。
如果 fromIndex 为负值，则表示从数组中的倒数第几个元素开始查找，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。即使该值为负，数组仍然会被从后向前查找。为负值时可视为length + start，此处length为数组的长度。
如果length + start仍然为负，则意味数组不会被查找，返回 -1。


**返回值**

lastIndexOf()方法的返回值为Number类型，返回给定元素在数组中最后一次被查找到的索引值，如果没有找到则返回 -1 。

注意： 
lastIndexOf()方法使用严格等于(“===”)判断 searchElement与数组中元素之间的等于关系。

**示例**

```
var array = [2, 5, 9, 2];
var index = array.lastIndexOf(2);    // index is 3
index = array.lastIndexOf(7);        // index is -1
index = array.lastIndexOf(2, 3);     // index is 3
index = array.lastIndexOf(2, 2);     // index is 0
index = array.lastIndexOf(2, -2);    // index is 0
index = array.lastIndexOf(2, -1);    // index is 3
```

使用lastIndexOf()查找到一个元素在数组中所有的索引，并使用push()将所有添加到另一个数组中

```
var indices = [];
var array = ['a', 'b', 'a', 'c', 'a', 'd'];
var element = 'a';
var idx = array.lastIndexOf(element);

while (idx != -1) {
  indices.push(idx);
  idx = (idx > 0 ? array.lastIndexOf(element, idx - 1) : -1);
}

console.log(indices);
// [4, 2, 0];
```

兼容

```
if (!Array.prototype.lastIndexOf) {
  Array.prototype.lastIndexOf = function(searchElement /*, fromIndex*/) {
    'use strict';

    if (this === void 0 || this === null) {
      throw new TypeError();
    }

    var n, k,
        t = Object(this),
        len = t.length >>> 0;
    if (len === 0) {
      return -1;
    }

    n = len - 1;
    if (arguments.length > 1) {
      n = Number(arguments[1]);
      if (n != n) {
        n = 0;
      }
      else if (n != 0 && n != (1 / 0) && n != -(1 / 0)) {
        n = (n > 0 || -1) * Math.floor(Math.abs(n));
      }
    }

    for (k = n >= 0
          ? Math.min(n, len - 1)
          : len - Math.abs(n); k >= 0; k--) {
      if (k in t && t[k] === searchElement) {
        return k;
      }
    }
    return -1;
  };
}
```