---
title: some()检测数组
date: 2018-02-21 23:11:02
tags:
  - Javascript
  - JS数组
---


**概述**
some()方法对数组中的每一项元素执行给定函数，如果该函数对任何一项返回 true，则返回 true，否则返回 false。

**语法**

```
array.some(callback, thisArg)
```

**参数**

```
callback	Function类型对每个数组元素执行的回调函数。
thisArg	可选/Object类型 指定回调函数内部的this指向。

```

注意：

some()方法中的 callback 回调函数默认支持 3 个参数，第 1 个是遍历的数组元素、第2个是元素对应的索引、第3个是数组本身。
如果为some()提供一个 thisArg 参数，该参数为调用 callback 时的 this 值。如果省略该参数，则 callback 被调用时的 this 值，在非严格模式下为全局对象，在严格模式下传入undefined。

some()方法的 callback 回调函数需要有返回值，这个返回值不必明确是布尔值类型 true 或 false。如果 callback 没有返回值，则视为返回 false。

```
var arr = [1, 2, 3, 4, 5];
arr.some(function(item){ console.log(item) });  // 返回false。 打印 1 2 3 4 5
arr.some(function(item){ return item });        // 返回true
```
callback只会在已经赋值的索引上执行，对于那些已经被删除或者从未被赋值的索引不会执行。请看下面示例：

```
var arr = [1, 2, 3, 4, 5, 6];
delete arr[2];
console.log(arr);    //  [1, 2, undefined, 4, 5, 6]

arr.some(function(item){ return item == undefined })  // false
arr.some(function(item){ return item > 0 })           // true
```

**返回值**

some()方法的返回值为Boolean类型，将原数组中的每个元素都按顺序执行一次 callback 函数，只要有任何一项元素执行结果返回 true，则some()方法返回 true。如果所有元素都返回 false，some()方法返回 false。

some()不会改变原数组。

some()遍历的元素的范围在第一次调用 callback 时就已经确定了。在调用some()后被添加到数组中的值不会被 callback 访问到。如果数组中存在的元素被更改，则他们传入 callback 的值是some()访问到他们那一刻的值。那些被删除的元素或从来未被赋值的元素将不会被访问到。

**示例**

```
//检测数组中是否有元素大于等于 10
function isBigEnough(element, index, array) {
  return (element >= 10);
}

var passed = [1, 5, 8, 3, 4].some(isBigEnough);
console.log(passed);       // true


var passed1 = [12, 54, 18, 130, 44].some(isBigEnough);
console.log(passed1);      // true
```

兼容

```
把下面的代码插入到脚本的开头来解决低级IE的兼容。
if (!Array.prototype.some)
{
  Array.prototype.some = function(fun /*, thisArg */)
  {
    'use strict';

    if (this === void 0 || this === null)
      throw new TypeError();

    var t = Object(this);
    var len = t.length >>> 0;
    if (typeof fun !== 'function')
      throw new TypeError();

    var thisArg = arguments.length >= 2 ? arguments[1] : void 0;
    for (var i = 0; i < len; i++)
    {
      if (i in t && fun.call(thisArg, t[i], i, t))
        return true;
    }

    return false;
  };
}
```