---
title: slice()提取数组子元素
date: 2018-02-08 11:22:21
tags:
  - Javascript
  - JS数组
---


**概述**
slice()方法把数组中一部分(连续的一段)提取复制到一个新的数组中，并返回这个新的数组。

**语法**

```
array.slice(start, end)
```

**参数**

```
start	Number类型从该索引处 (包含该索引元素) 开始提取原数组中元素。
end	可选/Number类型在该索引处 (不包含该索引元素) 结束提取原数组中元素。
```
注意:

如果 start 为负，则表示从原数组中的倒数第几个元素开始提取，也就是说，-1 指最后一个元素，-2 指倒数第二个元素，以此类推。为负时可视为length + start，此处length为数组的长度。
如果 end 为负，则表示从原数组中的倒数第几个元素结束提取，同上可视为length + end，此处length为数组的长度。
如果 end 被省略，则slice()会一直提取到原数组末尾。即end = length。
如果 end <= start，则不会提取任何元素复制到新数组中，返回一个空数组。
如果 start和end 同时被省略，则从原数组索引 0 到最后一个元素完整提取，相当于浅复制整个数组。

**返回值**

slice()方法的返回值为Array类型, 返回当前数组中索引 start (包含索引 start 元素) 到索引 end (不包括索引 end 元素)部分的元素组成的数组。
slice()方法不会改变调用它的数组。

**示例**

```
var arr = ['萤光之烛', 2018, true, 1234];

// 提取索引 1 , 3 的部分(不包括索引0,2)
console.log(arr.slice(1,3))       // [2018, true]


// start 为负  等价于 -3 + length = 1
console.log(arr.slice(-3,3))      // [2018, true]

// 省略 end
console.log(arr.slice(1))         // [2018, true, 1234]

//end <= start 时返回空数组
console.log(arr.slice(3,2))       // []

// 无参数
console.log(arr.slice())          // ["萤光之烛", 2018, true, 1234]
```
