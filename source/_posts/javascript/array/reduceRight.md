---
title: reduceRight()倒序迭代
date: 2018-02-20 11:31:22
tags:
  - Javascript
  - JS数组
---

**概述**
reduceRight()方法对数组中的每个元素（从右到左）开始执行给定函数，构建一个最终返回值。。reduceRight()方法和reduce()的执行方向相反。

**语法**

```
array.reduceRight(callback, initialValue)
```

**参数**

```
callback	Function类型对每个数组元素执行的回调函数。
initialValue	可选/任意类型作为首次调用 callback 的第一个参数。

```
reduceRight()方法中的 callback 回调函数默认支持 4 个参数。

第 1 个(previousValue)： 上一次执行 callback 的返回值；
第 2 个(currentValue): 数组中当前被处理的元素；
第 3 个(index)： 当前被处理元素的索引值；
第 4 个(array)： 调用reduceRight()方法的数组本身。

首次执行 callback 函数时，如果指定了 initialValue ，则使用 initialValue 作为 callback 的第一个参数(previousValue)，数组中最后一个元素作为第二个参数(currentValue)；如果没指定 initialValue，则用数组的最后一个元素作为 previousValue，倒数第二个元素作为 currentValue。

如果数组为空并且没有提供 initialValue， 会抛出TypeError。如果数组仅有一个元素（无论位置如何）并且没有提供 initialValue， 或者有提供 initialValue 但是数组为空，那么此唯一值将被返回并且callback不会被执行。

callback只会在已经赋值的索引上执行，对于那些已经被删除或者从未被赋值的索引不会执行。请看下面示例：

```
var arr = [1, 2, 3, 4, 5, 6];
delete arr[2];
console.log(arr);   //  [1, 2, undefined, 4, 5, 6]

arr.reduceRight(function(pre,cur){ return String(pre) + String(cur) })  // "65421"
```

每次的参数和返回值如下表：

```
迭代历程	  previous current index       array            return value
第1次调用     6         5     5   [1,2, undefined, 4,5,6]    65
第2次调用     65        4     3   [1,2, undefined, 4,5,6]    654
第3次调用     654       2     1   [1,2, undefined, 4,5,6]    6542
第4次调用     6542      1     0   [1,2, undefined, 4,5,6]    65421
```

**返回值**

reduceRight()方法的返回值为任意类型，从数组的最后一项开始，逐个遍历到第一个，由 callback 回调函数构建一个最终返回值。

reduceRight()不会改变原数组。

**示例**

```
   var total = [0, 1, 2, 3, 4].reduceRight(function(a, b) { return a + b });     // 10
```

```

迭代历程	  previous current index   array  return value
第1次调用     4         3     3   [0,1,2,3,4]    7
第2次调用     7         2     2   [0,1,2,3,4]    9
第3次调用     9         1     1   [0,1,2,3,4]    10
第4次调用     10        0     0   [0,1,2,3,4]    10
```
给reduceRight()传入第二个参数 10 。

```
var total = [0, 1, 2, 3, 4].reduceRight(function(a, b) { return a + b }, 10); // 20
```

```
迭代历程	  previous current index   array   return value
第1次调用     10         4     4   [0,1,2,3,4]    14
第2次调用     14         3     3   [0,1,2,3,4]    17
第3次调用     17         2     2   [0,1,2,3,4]    19
第4次调用     19         1     1   [0,1,2,3,4]    20
第5次调用     20         0     0   [0,1,2,3,4]    20
```
将数组扁平化。

```
var flattened = [[0, 1], [2, 3], [4, 5]].reduceRight(function(a, b) {
    return a.concat(b);
});
// flattened 为 [4, 5, 2, 3, 0, 1]
```

```
迭代历程  previousValue  currentValue  index  	array  		      return value
第1次调用    [4, 5]         [2, 3]       1   [[0, 1], [2, 3], [4, 5]]  [4, 5, 2, 3]
第2次调用  [4, 5, 2, 3]     [0, 1]       0   [[0, 1], [2, 3], [4, 5]]  [4, 5, 2, 3, 0, 1]
```

兼容

```
把下面的代码插入到脚本的开头来解决低级IE的兼容。
if ( 'function' !== typeof Array.prototype.reduceRight ) {
  Array.prototype.reduceRight = function( callback /*, initialValue*/ ) {
    'use strict';
    if ( null === this || 'undefined' === typeof this ) {
      throw new TypeError(
         'Array.prototype.reduce called on null or undefined' );
    }
    if ( 'function' !== typeof callback ) {
      throw new TypeError( callback + ' is not a function' );
    }
    var t = Object( this ), len = t.length >>> 0, k = len - 1, value;
    if ( arguments.length >= 2 ) {
      value = arguments[1];
    } else {
      while ( k >= 0 && ! k in t ) k--;
      if ( k < 0 )
        throw new TypeError('Reduce of empty array with no initial value');
      value = t[ k-- ];
    }
    for ( ; k >= 0 ; k-- ) {
      if ( k in t ) {
         value = callback( value, t[k], k, t );
      }
    }
    return value;
  };
}
```