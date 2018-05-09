---
title: reduce()迭代数组
date: 2018-02-19 16:01:02
tags:
  - Javascript
  - JS数组
---

**概述**
reduce()方法对数组中的每个元素（从左到右）开始执行给定函数，构建一个最终返回值。reduce()是所有数组方法中最为复杂的一个。

**语法**

```
array.reduce(callback, initialValue)
```

**参数**

```
callback	Function类型对每个数组元素执行的回调函数。
initialValue	可选/任意类型作为首次调用 callback 的第一个参数。

```
reduce()方法中的 callback 回调函数默认支持 4 个参数。

第 1 个(previousValue)： 上一次执行 callback 的返回值；
第 2 个(currentValue): 数组中当前被处理的元素；
第 3 个(index)： 当前被处理元素的索引值；
第 4 个(array)： 调用reduce()方法的数组本身。

首次执行 callback 函数时，如果指定了 initialValue ，则使用 initialValue 作为 callback 的第一个参数(previousValue)，数组中第一个元素作为第二个参数(currentValue)；如果没指定 initialValue，则用数组的第一个元素作为 previousValue，第二个元素作为 currentValue。

如果数组为空并且没有提供 initialValue， 会抛出TypeError。如果数组仅有一个元素（无论位置如何）并且没有提供 initialValue， 或者有提供 initialValue 但是数组为空，那么此唯一值将被返回并且callback不会被执行。

callback只会在已经赋值的索引上执行，对于那些已经被删除或者从未被赋值的索引不会执行。请看下面示例：

```
var arr = [1, 2, 3, 4, 5, 6];
delete arr[2];
console.log(arr);   // [1, 2, undefined, 4, 5, 6]

arr.reduce(function(pre,cur){ return String(pre) + String(cur) });  // "12456"
```

每次的参数和返回值如下表：

```
迭代历程	  previous current index       array            return value
第1次调用     1         2     1   [1,2, undefined, 4,5,6]    12
第2次调用     12        4     3   [1,2, undefined, 4,5,6]    124
第3次调用     124       5     4   [1,2, undefined, 4,5,6]    1245
第4次调用     1245      6     5   [1,2, undefined, 4,5,6]    12456
```

**返回值**

reduce()方法的返回值为任意类型，从数组的第一项开始，逐个遍历到最后，由 callback 函数构建一个最终返回值。

reduce()不会改变原数组。

**示例**

    var total = [0, 1, 2, 3, 4].reduce(function(a, b) { return a + b });     // 10

```

迭代历程	  previous current index       array    return value
第1次调用     0         1     1       [0,1,2,3,4]    1
第2次调用     1         2     2       [0,1,2,3,4]    3
第3次调用     3         3     3       [0,1,2,3,4]    6
第4次调用     6         4     4       [0,1,2,3,4]    10
```
给reduce()传入第二个参数 10 。
```
var total = [0, 1, 2, 3, 4].reduce(function(a, b) { return a + b }, 10); // 20
```

```
迭代历程	  previous current index  array    return value
第1次调用     10        0     0   [0,1,2,3,4]    10
第2次调用     10        1     1   [0,1,2,3,4]    11
第3次调用     11        2     2   [0,1,2,3,4]    13
第4次调用     13        3     3   [0,1,2,3,4]    16
第5次调用     16        4     4   [0,1,2,3,4]    20
```

将数组扁平化。

```
var flattened = [[0, 1], [2, 3], [4, 5]].reduce(function(a, b) {
    return a.concat(b);
});
// flattened 为 [0, 1, 2, 3, 4, 5]
```

```
迭代历程	previousValue	currentValue	index		array		return value
第1次调用   [0, 1]          [2, 3]          1    [[0, 1], [2, 3], [4, 5]]  [0, 1, 2, 3]
第2次调用   [0, 1, 2, 3]    [4, 5]          2    [[0, 1], [2, 3], [4, 5]]  [0, 1, 2, 3, 4, 5]
```

兼容

```
把下面的代码插入到脚本的开头来解决低级IE的兼容。
if ('function' !== typeof Array.prototype.reduce) {
  Array.prototype.reduce = function(callback, opt_initialValue){
    'use strict';
    if (null === this || 'undefined' === typeof this) {
      // At the moment all modern browsers, that support strict mode, have
      // native implementation of Array.prototype.reduce. For instance, IE8
      // does not support strict mode, so this check is actually useless.
      throw new TypeError(
          'Array.prototype.reduce called on null or undefined');
    }
    if ('function' !== typeof callback) {
      throw new TypeError(callback + ' is not a function');
    }
    var index, value,
        length = this.length >>> 0,
        isValueSet = false;
    if (1 < arguments.length) {
      value = opt_initialValue;
      isValueSet = true;
    }
    for (index = 0; length > index; ++index) {
      if (this.hasOwnProperty(index)) {
        if (isValueSet) {
          value = callback(value, this[index], index, this);
        }
        else {
          value = this[index];
          isValueSet = true;
        }
      }
    }
    if (!isValueSet) {
      throw new TypeError('Reduce of empty array with no initial value');
    }
    return value;
  };
}
```