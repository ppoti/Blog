---
title: indexOf()查找元素第一次的索引
date: 2018-02-17 11:34:31
tags:
  - Javascript
  - JS数组
---


**概述**
indexOf()方法用于查找给定元素在当前数组中第一次出现的位置。

**语法**

```
array.indexOf(searchElement, fromIndex)
```

**参数**

```
searchElement	任意类型要在数组中查找的元素。
fromIndex	可选/Number类型 指定从数组中开始查找的索引位置。

```

注意：

如果 fromIndex 的值大于数组长度，则意味不在数组中查找，返回 -1。
如果 fromIndex 为负值，则表示从数组中的倒数第几个元素开始查找，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。为负值时可视为length + start，此处length为数组的长度。


**返回值**

indexOf()方法的返回值为Number类型，返回给定元素在数组中第一次被查找到的索引值，如果没有找到则返回 -1 。

注意： 
indexOf()方法使用严格等于(“===”)判断 searchElement 与数组中元素之间的等于关系。

**示例**

```
var array = [2, 5, 9];
array.indexOf(2);       // 0
array.indexOf(7);       // -1
array.indexOf(9, 2);    // 2
array.indexOf(2, -1);   // -1
array.indexOf(2, -3);   // 0
```

兼容

```
把下面的代码插入到脚本的开头来解决低级IE的兼容。
// Production steps of ECMA-262, Edition 5, 15.4.4.14
// Reference: http://es5.github.io/#x15.4.4.14
if (!Array.prototype.indexOf) {
  Array.prototype.indexOf = function(searchElement, fromIndex) {

    var k;

    // 1. Let O be the result of calling ToObject passing
    //    the this value as the argument.
    if (this == null) {
      throw new TypeError('"this" is null or not defined');
    }

    var O = Object(this);

    // 2. Let lenValue be the result of calling the Get
    //    internal method of O with the argument "length".
    // 3. Let len be ToUint32(lenValue).
    var len = O.length >>> 0;

    // 4. If len is 0, return -1.
    if (len === 0) {
      return -1;
    }

    // 5. If argument fromIndex was passed let n be
    //    ToInteger(fromIndex); else let n be 0.
    var n = +fromIndex || 0;

    if (Math.abs(n) === Infinity) {
      n = 0;
    }

    // 6. If n >= len, return -1.
    if (n >= len) {
      return -1;
    }

    // 7. If n >= 0, then Let k be n.
    // 8. Else, n<0, Let k be len - abs(n).
    //    If k is less than 0, then let k be 0.
    k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);

    // 9. Repeat, while k < len
    while (k < len) {
      // a. Let Pk be ToString(k).
      //   This is implicit for LHS operands of the in operator
      // b. Let kPresent be the result of calling the
      //    HasProperty internal method of O with argument Pk.
      //   This step can be combined with c
      // c. If kPresent is true, then
      //    i.  Let elementK be the result of calling the Get
      //        internal method of O with the argument ToString(k).
      //   ii.  Let same be the result of applying the
      //        Strict Equality Comparison Algorithm to
      //        searchElement and elementK.
      //  iii.  If same is true, return k.
      if (k in O && O[k] === searchElement) {
        return k;
      }
      k++;
    }
    return -1;
  };
}
```