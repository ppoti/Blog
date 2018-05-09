---
title: forEach()数组循环
date: 2018-02-14 10:07:13
tags:
  - Javascript
  - JS数组
---


**概述**
forEach()方法让数组中每个元素都执行一次给定的函数

**语法**

```
array.forEach(callback, thisArg)
```

**参数**

```
callback	Function类型对每个数组元素执行的回调函数。
thisArg	可选/Object类型 指定回调函数内的this指向。

```

注意： 
forEach()方法中的 callback 回调函数默认支持 3 个参数，第 1 个是遍历的数组元素、第2个是元素对应的索引、第3个是数组本身。
如果为forEach()提供一个 thisArg 参数，该参数为调用 callback 时的 this 值。如果省略该参数，则 callback 被调用时的 this 值，在非严格模式下为全局对象，在严格模式下传入undefined。

callback只会在已经赋值的索引上执行，对于那些已经被删除或者从未被赋值的索引不会执行。请看下面示例：

```
var arr = [1, 2, 3, 4, 5, 6];
delete arr[2];
console.log(arr)   //  [1, 2, undefined, 4, 5, 6]

arr.forEach(function(item){ console.log(item); })  //依次打印 1 2 4 5 6
```

**返回值**

forEach()仅仅遍历数组每个元素执行一次 callback 函数，它没有返回内容。这一点和map()方法、some()方法、every()方法不同。如果打印forEach()方法返回内容，会出现undefined。

forEach()不会改变原数组。

forEach()遍历的元素的范围在第一次调用 callback 时就已经确定了。在调用forEach()后被添加到数组中的值不会被 callback 访问到。如果数组中存在的元素被更改，则他们传入 callback 的值是forEach()访问到他们那一刻的值。那些被删除的元素或从来未被赋值的元素将不会被访问到。

**示例**

```
var letters = ['a', 'b', 'c']; 

var fun = function (element, index, array) {
  console.log(element.toUpperCase());
};

letters.forEach(fun);  //  依次打印出  A   B   C
```

上面有说到forEach()方法不返回任何内容。

```
var letters = ['a', 'b', 'c']; 

var fun = function (element, index, array) {
  return element.toUpperCase();
};

console.log(letters.forEach(fun));       //打印结果  undefined
```
如有需要，可使用map()方法。

```
var letters = ['a', 'b', 'c']; 

var fun = function (element, index, array) {
  return element.toUpperCase();
};

console.log(letters.map(fun));           // ["A", "B", "C"]
```

兼容

```
// Production steps of ECMA-262, Edition 5, 15.4.4.18
// Reference: http://es5.github.com/#x15.4.4.18
if ( !Array.prototype.forEach ) {

  Array.prototype.forEach = function forEach( callback, thisArg ) {

    var T, k;

    if ( this == null ) {
      throw new TypeError( "this is null or not defined" );
    }

    // 1. Let O be the result of calling ToObject passing the |this| value as the argument.
    var O = Object(this);

    // 2. Let lenValue be the result of calling the Get internal method of O with the argument "length".
    // 3. Let len be ToUint32(lenValue).
    var len = O.length >>> 0; 

    // 4. If IsCallable(callback) is false, throw a TypeError exception.
    // See: http://es5.github.com/#x9.11
    if ( typeof callback !== "function" ) {
      throw new TypeError( callback + " is not a function" );
    }

    // 5. If thisArg was supplied, let T be thisArg; else let T be undefined.
    if ( arguments.length > 1 ) {
      T = thisArg;
    }

    // 6. Let k be 0
    k = 0;

    // 7. Repeat, while k < len
    while( k < len ) {

      var kValue;

      // a. Let Pk be ToString(k).
      //   This is implicit for LHS operands of the in operator
      // b. Let kPresent be the result of calling the HasProperty internal method of O with argument Pk.
      //   This step can be combined with c
      // c. If kPresent is true, then
      if ( k in O ) {

        // i. Let kValue be the result of calling the Get internal method of O with argument Pk.
        kValue = O[ k ];

        // ii. Call the Call internal method of callback with T as the this value and
        // argument list containing kValue, k, and O.
        callback.call( T, kValue, k, O );
      }
      // d. Increase k by 1.
      k++;
    }
    // 8. return undefined
  };
}
```