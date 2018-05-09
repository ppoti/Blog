---
title: join()元素分隔
date: 2018-02-03 07:23:01
tags:
  - Javascript
  - JS数组
---

**概述**
join()方法将当前数组的所有元素以指定的分隔符连接起来组成字符串

**语法**

```
array.join(separator)
```

**参数**

```
separator	可选/String类型指定要使用的分隔符。
```
注意：
如果参数为空(没有指定分隔符)则用默认逗号作为分隔符。 
如果参数为空字符串则数组中元素直接相连。 
参数应为String类型，如果不是，则会对参数调用toString()方法将其转为字符串。

**返回值**
join()方法的返回值为String类型，返回数组中所有元素以指定的分隔符连接起来所组成的字符串。如果数组中没有元素，则返回空字符串。

**示例**

```
var Array = ['Tody', 'Yestady', 'Tomorrow'];
var Array1 = Array.join();         // Array1 "Tody,Yestady,Tomorrow"
var Array2 = Array.join(', ');     // Array2的值变为 "Tody, Yestady, Tomorrow"
var Array3 = Array.join(' + ');    // Array3的值变为 "Tody + Yestady + Tomorrow"
var Array4 = Array.join('');       // Array4的值变为 "TodyYestadyTomorrow"

// 对{}调用toString()方法 
var Array5 = Array.join({})        // Array4的值变为 "Tody[object Object]Yestady[object Object]Tomorrow"
```
```