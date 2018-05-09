---
title: filter()检测数组
date: 2018-02-13 20:37:13
tags:
  - Javascript
categories:
  - JS数组方法
  - Array
---


**概述**
filter()方法对数组中的每一项元素执行给定函数，并返回一个由执行该函数时返回 true 的元素组成的新数组。

**语法**

```
array.filter(callback, thisArg)
```

**参数**

```
callback	Function类型对每个数组元素执行的回调函数。
thisArg	可选/Object类型 指定回调函数内部的this指向。

```

注意： 
filter()方法中的 callback 回调函数默认支持 3 个参数，第 1 个是遍历的数组元素、第2个是元素对应的索引、第3个是数组本身。
如果为filter()提供一个 thisArg 参数，该参数为调用 callback 时的 this 值。如果省略该参数，则 callback 被调用时的 this 值，在非严格模式下为全局对象，在严格模式下传入undefined。

filter()方法的 callback 回调函数需要有返回值，这个返回值不必明确是布尔值类型 true 或 false。如果 callback 没有返回值，则视为返回 false。

```
var arr = [0, 1, 2, 3, 4, 5];

var arr1 = arr.filter(function(item){ console.log(item) });
 // arr1为空数组       // 打印 0 1 2 3 4 5

var arr2 = arr.filter(function(item){return item });
 // arr2为 [1, 2, 3, 4, 5]
```

callback只会在已经赋值的索引上执行，对于那些已经被删除或者从未被赋值的索引不会执行。请看下面示例：

```
var arr = [1, 2, 3, 4, 5, 6];
delete arr[2];
console.log(arr);   //  [1, 2, undefined, 4, 5, 6]

arr.filter(function(item){ return item == undefined })  // 空数组 []
arr.filter(function(item){ return item > 0 })           // [1, 2, 4, 5, 6]
```

**返回值**

filter()方法的返回值为Array类型，将原数组中每个元素执行一次 callback 函数，把每次执行后返回 true 的元素组合起来形成一个新数组，fliter()方法返回值就是这个新数组。如果素所有元素运行函数时都返回 false，则返回空数组 []。

filter()不会改变原数组。

filter()遍历的元素的范围在第一次调用 callback 时就已经确定了。在调用filter()后被添加到数组中的值不会被 callback 访问到。如果数组中存在的元素被更改，则他们传入 callback 的值是filter()访问到他们那一刻的值。那些被删除的元素或从来未被赋值的元素将不会被访问到。

**示例**

```
//提取出数组中大于等于 10 的元素
function isBigEnough(element, index, array) {
  return (element >= 10);
}

var passed = [1, 5, 8, 3, 4].filter(isBigEnough);
console.log(passed)       // 空数组 []


var passed1 = [12, 5, 8, 130, 44].filter(isBigEnough);
console.log(passed1)      // [12, 130, 44] 
```

兼容

```
//把下面的代码插入到脚本的开头来解决低级IE的兼容。
if (!Array.prototype.filter)
{
  Array.prototype.filter = function(fun /*, thisArg */)
  {
    "use strict";

    if (this === void 0 || this === null)
      throw new TypeError();

    var t = Object(this);
    var len = t.length >>> 0;
    if (typeof fun !== "function")
      throw new TypeError();

    var res = [];
    var thisArg = arguments.length >= 2 ? arguments[1] : void 0;
    for (var i = 0; i < len; i++)
    {
      if (i in t)
      {
        var val = t[i];
        if (fun.call(thisArg, val, i, t))
          res.push(val);
      }
    }

    return res;
  };
}
```