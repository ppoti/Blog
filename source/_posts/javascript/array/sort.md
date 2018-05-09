---
title: sort()数组排序
date: 2018-02-09 09:11:08
tags:
  - Javascript
  - JS数组
---


**概述**
sort()方法用于将当前数组对象的元素按指定顺序进行排序，并返回排序后的数组。

**语法**

```
array.sort(compareFunction)
```

**参数**

```
compareFunction	可选/Function类型指定如何比较元素顺序的函数。
```
注意:

如果省略compareFunction参数，元素将按ASCII字符顺序的升序进行排列。
如果提供了compareFunction参数，那么数组会按照调用该函数的返回值排序。记 a 和 b 是两个将要被比较的元素：

如果 compareFunction(a, b) 小于 0 ， a 会被排列到 b 之前；
如果 compareFunction(a, b) 等于 0 ， a 和 b 的相对位置不变；
如果 compareFunction(a, b) 大于 0 ， b 会被排列到 a 之前。
sort()方法对数组如何排序完全取决于compareFunction函数，例如对数组[1,4,3,2,5] 排序。
升序，小的在前大的在后：compareFunction(a, b){return a-b}
降序，大的在前小的在后：compareFunction(a, b){return b-a}

**返回值**

sort()方法的返回值为Array类型，返回排序后的数组对象。
在排序过程中，并不会创建新的数组对象，返回的数组对象就是经过排序后的当前数组本身。

**示例**

```
var arr = ['萤光之烛', 2018, true, 1234];

// 按照ASCII字符顺序进行升序排列
console.log(arr.sort());               // [1234, 2018, "萤光之烛", true]

var arr1 = [12,5,8,3,2,14];
//  升序排列
function compareNumbers(a, b) {
  return a - b;
}

console.log(arr1.sort(compareNumbers)) // [2, 3, 5, 8, 12, 14] 
```
sort()方法可以使用函数表达式方便地书写：

```
var numbers = [4, 2, 5, 1, 3];

numbers.sort(function(a, b) {
  return a - b;
});
console.log(numbers);         // [1, 2, 3, 4, 5]

numbers.sort(function(a, b) {
  return b - a;
});

console.log(numbers);         // [5, 4, 3, 2, 1]
```
对象可以按照某个属性排序

```
var items = [
  { name: 'Edward', value: 21 },
  { name: 'Sharpe', value: 37 },
  { name: 'And', value: 45 },
  { name: 'The', value: -12 },
  { name: 'Magnetic' , value: 99 },
  { name: 'Zeros', value: 37 }
];

items.sort(function (a, b) {
  if (a.value > b.value) {
    return 1;
  }
  if (a.value < b.value) {
    return -1;
  }

  return 0;
});


// 0 : {name: "The", value: -12}
// 1 : {name: "Edward", value: 21}
// 2 : {name: "Sharpe", value: 37}
// 3 : {name: "Zeros", value: 37}
// 4 : {name: "And", value: 45}
// 5 : {name: "Magnetic", value: 99}

```
