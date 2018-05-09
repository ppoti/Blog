---
title: splice()移除/替换数组
date: 2018-02-10 09:07:57
tags:
  - Javascript
  - JS数组
---


**概述**
splice()方法用于从当前数组中移除一部分连续的元素。如有需要，还可以在所移除元素的位置上插入一个或多个新的元素。该方法以数组形式返回当前数组中被移除的元素

**语法**

```
array.splice(start, deleteCount, item1, item2,...itemN)
```

**参数**

```
start	Number类型从数组中移除元素操作的起点索引。
deleteCount	Number类型需要移除的元素个数。
itemN	可选/任意类型要添加到数组中元素被移除位置的新元素，可以有多个。

```
注意:

splice()方法从索引 start 开始，移除 deleteCount 个元素(包含 start 索引元素)，在 start 索引处插入 itemN 。

如果 start >= length ，则不会移除任何元素，返回一个空数组。
如果 start 是负值，则表示从数组的倒数第几位开始移除元素。可视为 length + start，此处length为数组的长度。
如果 deleteCount 为 0 或负数，则不会移除任何元素，返回一个空数组。
如果参数 itemN 为数组类型(Array)，仍会被当作一个元素看待，插入到当前数组中。

**返回值**

splice()方法的返回值为Array类型，返回当前数组中被移除的元素所组成的新数组。
当移除数组中的元素时，数组的length属性也会随之改变。一般而言，数组的length属性将会减N(N为实际移除的元素个数)。

**示例**

```
var arr = ['萤光之烛', 2018, true, 1234, -1024, 10];

// 从索引 2 开始，移除 3 个元素
var res = arr.splice(2,3);
console.log(arr);          // ["萤光之烛", 2018, 10] 
console.log(res);          // [true, 1234, -1024]


// 从索引 1 开始，移除 2 个元素，插入两个元素
var res1 = arr.splice(1, 2, 'newitem1', 'newitem2');

console.log(arr);          // ["萤光之烛", "newitem1", "newitem2"] 
console.log(res1);         // [2018, 10]


// 从索引 1 开始，移除 0 个元素，插入两个元素
var res2 = arr.splice(1, 0, 'abc', 'xyz');

console.log(arr);          // ["萤光之烛", "abc", "xyz", "newitem1", "newitem2"]        
console.log(res2);         // 返回空数组 []
```