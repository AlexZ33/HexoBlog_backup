---
title: js闭包
date: 2016-03-07 18:44:12
tags:
- javascript
- 闭包
- wiki
- 日志
- 前端
categories: 前端
---
<b>js闭包<b>

闭包
（1）概念
闭包是指有权访问另一个函数作用域中的变量的函数。
（2）特性
闭包只能取得包含函数中任何变量的最后一个值。
（3）创建方式
在一个函数内部创建另一个函数。
（4）原理
在一个函数内部中定义的函数会将包含函数（外部函数）的活动对象添加到其作用域中，直至解除对内部函数的应用，内部函数被销毁，外部函数的活动对象才会被销毁。
（5）实例

```
function closure(){
    var result=[];
    for (var i = 0; i < 4; i++) {
        result[i]=function(){
            console.log(i);
            return i;
        }
    };
    return result;
}
var result=closure();
for (var i = 0; i < 4; i++) {
    result[i]();
};

//4 4 4 4
```

