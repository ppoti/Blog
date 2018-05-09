---
title: map()返回新数组
date: 2018-02-16 13:37:33
tags:
  - Javascript
  - JS数组
---

**概述**
map()方法返回一个由原数组中每个元素执行给定函数的返回值组成的新数组。

**语法**

```
array.map(callback, thisArg)
```

**参数**

```
callback	Function类型对每个数组元素执行的回调函数。
thisArg	可选/Object类型 指定回调函数内部的this指向。

```

注意：

map()方法中的 callback 回调函数默认支持 3 个参数，第 1 个是遍历的数组元素、第2个是元素对应的索引、第3个是数组本身。
如果为map()提供一个 thisArg 参数，该参数为调用 callback 时的 this 值。如果省略该参数，则 callback 被调用时的 this 值，在非严格模式下为全局对象，在严格模式下传入undefined。

map()的 callback 函数需要有返回值，这些返回值组成新数组作为map()方法的返回值。如果回调函数没有返回值，则视为返回undefined。

```
var arr = [0, 1, 2, 3, 4, 5];

var arr1 = arr.map(function(item){ console.log(item) });
//打印 0 1 2 3 4 5 // arr1为[undefined, undefined, undefined, undefined, undefined, undefined]
```
callback只会在已经赋值的索引上执行，对于那些已经被删除或者从未被赋值的索引不会执行。请看下面示例：

```
var arr = [1, 2, 3, 4, 5, 6];
delete arr[2];
console.log(arr)   //  [1, 2, undefined, 4, 5, 6]

arr.map(function(item){ return Boolean(item) })  // [true, true, undefined × 1, true, true, true]
```

**返回值**

map()方法的返回值为Array类型，对数组中的每个元素都按顺序执行一次 callback 函数，将每次执行 callback 的返回值组成一个新数组。这个新书组就是map()方法的返回值。

map()不会改变原数组。

map()遍历的元素的范围在第一次调用 callback 时就已经确定了。在调用map()后被添加到数组中的值不会被 callback 访问到。如果数组中存在的元素被更改，则他们传入 callback 的值是map()访问到他们那一刻的值。那些被删除的元素或从来未被赋值的元素将不会被访问到。

**示例**

```
//对数组中每个元素求平方
var arr = [1, 5, 8, 3, 4];

var arrayOSquares = arr.map(function(item){ return item * item });

console.log(arrayOSquares)       // [1, 25, 64, 9, 16]
```


一般情况下，map()方法中的 callback 函数只需要接受一个参数，就是正在被遍历的数组元素本身。但这并不意味着map()只给 callback 传了一个参数。这个思维惯性可能会让我们犯一个很容易犯的错误。

```
['1', '2', '3'].map(parseInt);
// 你可能觉的会是 [1, 2, 3]
// 但实际的结果是 [1, NaN, NaN]
```

通常使用parseInt()方法时，只需要传递一个参数。但实际上parseInt()可以有两个参数。第二个参数是进制数。可以通过语句”alert(parseInt.length)===2”来验证。map()方法在调用 callback 函数时，会给它传递三个参数：当前正在遍历的元素, 元素索引, 原数组本身。第三个参数parseInt()会忽视, 但第二个参数不会，也就是说，parseInt()把传过来的索引值当成进制数来使用。从而返回了NaN。

```
parseInt("1",0)   // 1
parseInt("2",1)   // NaN
parseInt("3",2)   // NaN

["1", "2", "3"].map(function(item){ return parseInt(item, 10) });
// [1, 2, 3]
```

兼容

```
// 实现 ECMA-262, Edition 5, 15.4.4.19
// 参考: http://es5.github.com/#x15.4.4.19
if (!Array.prototype.map) {
  Array.prototype.map = function(callback, thisArg) {

    var T, A, k;

    if (this == null) {
      throw new TypeError(" this is null or not defined");
    }

    // 1. 将O赋值为调用map方法的数组.
    var O = Object(this);

    // 2.将len赋值为数组O的长度.
    var len = O.length >>> 0;

    // 3.如果callback不是函数,则抛出TypeError异常.
    if (Object.prototype.toString.call(callback) != "[object Function]") {
      throw new TypeError(callback + " is not a function");
    }

    // 4. 如果参数thisArg有值,则将T赋值为thisArg;否则T为undefined.
    if (thisArg) {
      T = thisArg;
    }

    // 5. 创建新数组A,长度为原数组O长度len
    A = new Array(len);

    // 6. 将k赋值为0
    k = 0;

    // 7. 当 k < len 时,执行循环.
    while(k < len) {

      var kValue, mappedValue;

      //遍历O,k为原数组索引
      if (k in O) {

        //kValue为索引k对应的值.
        kValue = O[ k ];

        // 执行callback,this指向T,参数有三个.分别是kValue:值,k:索引,O:原数组.
        mappedValue = callback.call(T, kValue, k, O);

        // 返回值添加到新数组A中.
        A[ k ] = mappedValue;
      }
      // k自增1
      k++;
    }

    // 8. 返回新数组A
    return A;
  };      
}
```