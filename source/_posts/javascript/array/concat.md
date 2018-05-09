---
title: concat() 连接数组
date: 2018-02-02 08:13:55
tags:
  - Javascript
  - JS数组
---

**概述**
concat()方法将传入的值与原数组合并，组成一个新的数组并返回，该方法不会改变调用它的数组。所有浏览器均支持该方法。

**语法**

```
array.concat(value1, value2, ..., valueN)
```

**参数**

```
value1	可选/任意类型添加到当前数组末尾处的数据项。
valueN	可选/任意类型要添加到当前数组末尾处的其他项，可以有多个。
```
注意：
如果参数为空，则返回一个当前数组的浅复制；
如果参数为数组类型(Array)，则将该参数数组中的所有元素依次拼接到当前数组的末尾；
如果是其他类型，则将其本身作为元素添加到当前数组的末尾处。

**返回值**
concat()方法的返回值为Array类型，返回由当前数组和其他项组合而成的新数组。concat()方法不会修改调用它的数组，而是将他们的每个元素复制一份放在组合成的新数组中。原数组中的元素有两种被复制的方式：

对象引用(引用类型数据)：concat()方法会复制对象引用放到组合的新数组中，原数组和新数组中的对象引用都指向同一个实际的对象，所以，当实际的对象被修改时，两个数组也同时会被修改。
字符串和数字值类型数据(是原始值，而不是包装原始值的 String 和 Number 对象)：concat() 方法会复制字符串和数字的值放到新数组中。

**示例**
将两个数组合并为新数组、将元素添加到数组。

```
var arr1 = [1, 2, 3];
var arr2 = ['萤光之烛', 2018];
var arr = arr1.concat(arr2);     // [1, 2, 3, "萤光之烛", 2018]  // arr1和arr2不变

var arr3 = arr1.concat('javascript');    // [1, 2, 3, "javascript"]
var arrs = ['abc', 2018, [1, 2, 3], '萤光之烛'];
var array = arr1.concat(arrs);
// [1, 2, 3, "abc", 2018, [1,2,3], "萤光之烛"]  这里拆分数组只拆了一层。
```
完全复制(值类型)

```
var arr = [2018, '萤光之烛', true];
var result = arr.concat();            // [2018, "萤光之烛", true]
```

浅复制(引用类型)

```
var obj = {
  domain: '萤光之烛',
  year: 2015
};

var arr1 = [1, 2, 3, obj];

var newresult = arr1.concat();   // [1, 2, 3, Object]
console.log(newresult[3].year)   // 2015

obj.year = 2018;

console.log(newresult[3].year)   // 2018

var arr2 = [1, 2, [11, 22]];
var arr3 = arr2.concat();
arr2[2][0] = '萤光之烛';
console.log(arr3[2][0])          // 2018
```