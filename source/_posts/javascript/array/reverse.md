---
title: reverse()颠倒数组中元素的顺序
date: 2018-02-06 18:22:12
tags:
  - Javascript
  - JS数组
---


**概述**
reverse()方法用于将当前数组的元素顺序全部反转，并返回元素顺序反转后的数组。

**语法**

```
array.reverse()
```

**返回值**
reverse()方法的返回值为Array类型，返回元素顺序被反转后的数组对象。

reverse()方法将当前数组对象中的元素按所在位置进行反转。在执行过程中，此方法并不创建新的Array对象，而是直接在当前对象上进行反转。返回的数组对象就是经过顺序反转后的当前对象。

如果数组是不连续的，reverse()方法将在数组中创建元素，这些元素将填充数组中的间隙。所创建的这些元素的值全部为undefined。

**示例**

```

var array = ['萤光之烛', 2018, true];
var res = array.reverse();
console.log(res);             // [true, 2018, '萤光之烛']
console.log(res === array);   // true

```
```