---
title: js几种事件处理程序
date: 2016-04-15 18:44:12
tags:
- javascript
- 事件处理程序
- 日志
- 前端
categories: 前端
---
<b>js几种事件处理程序<b>

[微信公众号阅读](https://mp.weixin.qq.com/s?__biz=MzI1MjA2NzQ3Ng==&mid=2457137471&idx=3&sn=5697c46c041a8497b554be2aee42f829&chksm=fe693ac4c91eb3d25ebbd7f339d15142782bcc17fc63857d30f8528169a62e070e1b14c927cc#rd)

事件就是用户或浏览器自身执行的某种动作，如click,laod,mouseover都是事件的名称。

事件流描述的是从页面中接收事件的顺序。

事件处理程序就是对事件作出响应的函数。事件处理程序的名字以“on”开头，如click事件对应的事件处理程序的名称为onclick。

为事件指定处理程序的方式有多种，如：**HTML事件处理程序、DMO0级事件处理程序、DOM2级事件处理程序、IE事件处理程序、跨浏览器事件处理程序。**

**（1）html事件处理程序**

即：将事件处理程序，写在相应的html标签中。
eg:

```
<input type="button" value="click me" onclick="alert("hello")" />
```

缺点：①存在一个时间差，当用户在html元素一出现在页面上就去触发相应的事件时，事件的处理程序可能还不具备执行条件（比如说调用的函数还木有被解析），就会引发错误。
eg:

```
<input type="button" value="click me" onclick="message()" />
<script type="text/JavaScript">
```
        function message(){ 
                alert("hello world");
        }
</script>

因为调用的函数处于按钮的下方，如果在message函数被加载之前就点击了按钮就会引发错误。
②html和js代码耦合度太高，如果要改变事件处理程序，就要改动两个地方：html代码和javascript代码。

**（2）DMO0级事件处理程序**
eg:

```
var btn=document.getElementById("myBtn");
 btn.onclick=function(){
            alert(this.id)
};
```

注意：如果这段代码位于按钮之后，就有可能在一点时间内怎么点击都木有反应，因为在这段代码运行以前不会指定事件处理程序。

DMO0级事件处理程序被认为是元素的方法，换句话说，DMO0级事件处理程序是在元素的作用域中运行的，所以程序中的this引用当前元素。可以在事件处理程序中通过this访问元素的任何属性和方法。
以这种方式添加的事件处理程序会在事件流的冒泡阶段被处理。

也可删除指定的事件处理程序，只要将事件处理程序的属性设置为null就Ok了。
eg:

```
btn.onclick=null;
```

将处理程序设置为null以后，再点击按钮不会发生任何动作。

**（3）DOM2级事件处理程序**

DOM2级事件定义了两个方法，用于指定和删除事件处理程序。这两个操作分别为：addEventListener()和removeEventListner().所有的DOM节点都包含这两个方法。他们要接受3个参数，分别为：要处理的事件名，处理函数，布尔值。最后的布尔值参数如果为ture,表示在捕获阶段处理程序，如果为false，表示在冒泡阶段调用事件处理程序。

![](http://on891bjlf.bkt.clouddn.com/image/640.jpg)

例如在按钮上为click添加事件处理程序，可以用下面的代码：

```
var btn=document.getElementById("myBtn");
btn.addEventListner("onclick",function(){
alert("hello world");false
});
//这里添加的事件处理程序也是依附于元素的的作用域
```

使用DOM2事件处理程序的优点是：可以为同一个元素添加多个事件处理程序。
例：

```
var btn=getElementById("myBtn");
	btn.addEventListner("click",function(){alert(this.id);},flase);
	btn.addEventListner("click",function(){alert("hello world");},flase);
```

结果：先显示id，后显示hello world。
通过addEventListner()添加的事件处理程序只能通过removeEventListner来删除。移除时使用的参数与添加事件处理程序的参数相同。另：通过addEventListner添加的匿名函数无法删除。

**（4）IE事件处理程序。**

IE添加和删除事件处理程序的函数分别为：attachEvent()和detachEvent();
这两个函数接收相同的两个参数：事件处理程序名与事件处理函数。由于IE只支持事件冒泡，所以通过attachEvent添加的事件处理程序都会添加到冒泡阶段。
例如：

```
var btn=document.getElementById("myBtn");
btn.attachEvent("onclick",function(){alert("hello world");});
```

IE在使用attachEvent方法的情况下，事件处理程序的作用域为全局作用域，因此this等于window。（在编写跨浏览器的代码时，记住这一点非常重要）。
与addEventListner类似，attachEvent()方法也可以用来为一个元素添加多个事件处理程序；
eg:

```
var btn=document.getElementById("myBtn");
btn.attachEvent("onclick",function(){alert("clicked");});
btn.attachEvent("onclick",function(){alert("hello world");});
```

值得注意的是：这些事件的处理程序是按逆序触发的，也就是说，先弹出hello world 再弹出clicked。
detach()使用方法略。

**（5）跨浏览器的事件处理程序**

为了以跨浏览器的方式处理事件，主要可以使用两个方法：
①使用能隔离浏览器差异的js库。
②自己编写最适合的事件处理方法。这里要用到能力检测，即：识别浏览器的能力。要保证代码能在大多数浏览器下一致的运行，只须关注冒泡阶段。

代码步骤如下：

首先要创建的方法是addHandler(用于处理跨浏览器的兼容性问题，这里没有给出具体代码),它的职责是视情况判定使用DOM0级方法，DOM2级方法，IE方法来添加事件。addHandler接收3个参数：要操作的元素、事件名称、事件处理程序函数。这个方法属于一个名叫EventUtil的对象。这里使用这个对象来处理浏览器之间的差异。
与addHandler对应的方法是removeHandler(),它也接受相同的参数。这个事件的职责是移除之前添加的事件处理程序。不论事件是以什么方式添加到对象中的，如果其他方法程序无效，则默认使用DOM0级方法。
使用EventUtil的方法如下：

```
var btn=document.getElementById("myBtn");
var handler=function(){alert("hello")};//事件处理程序
EventUtil.addHandler(btn,"onclick",handler);

//其他代码
EventUtil.removeHandler(btn,"onclick",handler);
addHandler()和removeHandler()
```

没有考虑到所有的浏览器问题，例如IE中作用域的问题，但是使用它们添加和移除事件处理程序还是足够了。

**参考：**

> 《javascript高级程序设计》13章
