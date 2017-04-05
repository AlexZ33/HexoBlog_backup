---
title: js实现放大镜特效
date: 2016-03-030 12:44:12
tags:
- javascript
- 网页常见特效
- 放大镜
- 前端
categories: 前端
---
<b>js实现放大镜特效<b>


**效果**
![](http://on891bjlf.bkt.clouddn.com/gif/%E6%94%BE%E5%A4%A7%E9%95%9C.gif)

**实现原理：**

鼠标在小图片上移动时，通过捕获鼠标在小图片上的位置，定位大图片的相应位置

**技术点**
- 事件捕获
	 - onmouseover
	 - onmouseout
	 - onmousemove
- 定位
	-  offsetLeft
	-  offsetTop
	-  offsetWidth
	-  offsetHeight
	-  event.clientX
	-  event.clientY
![](http://on891bjlf.bkt.clouddn.com/image/%E6%88%AA%E5%9B%BE1491364873.png)
![](http://on891bjlf.bkt.clouddn.com/image/%E6%88%AA%E5%9B%BE1491365021.png)
- 计算
![](http://on891bjlf.bkt.clouddn.com/%E6%88%AA%E5%9B%BE1491389316.png)
- 浏览器兼容性

问号部分即：
objBigBoxImage.style.left
很容易求出  

同理可以求出
objBigBoxImage.style.top

**源码**
[github clone地址:](https://github.com/AlexZ33/commom_special_efficiency)
```
    <!doctype html>
<html>
<head>
    <meta charset="UTF-8">
    <title>放大镜</title>
    <style>
        * {
            margin: 0;
            padding: 0
        }

        #demo {
            display: block;
            width: 400px;
            height: 255px;
            margin: 50px;
            position: relative;
            border: 1px solid #ccc;
        }

        #small-box {
            position: relative;
            z-index: 1;
        }

        #float-box {
            display: none;
            width: 160px;
            height: 120px;
            position: absolute;
            background: #ffffcc;
            border: 1px solid #ccc;
            filter: alpha(opacity=50);
            opacity: 0.5;
        }

        #mark {
            position: absolute;
            display: block;
            width: 400px;
            height: 255px;
            background-color: #fff;
            filter: alpha(opacity=0);
            opacity: 0;
            z-index: 10;
        }

        #big-box {
            display: none;
            position: absolute;
            top: 0;
            left: 460px;
            width: 400px;
            height: 300px;
            overflow: hidden;
            border: 1px solid #ccc;
            z-index: 1;;
        }

        #big-box img {
            position: absolute;
            z-index: 5
        }
    </style>
    <script>

        //页面加载完毕后执行
        window.onload = function () {

            var objDemo = document.getElementById("demo");
            var objSmallBox = document.getElementById("small-box");
            var objMark = document.getElementById("mark");
            var objFloatBox = document.getElementById("float-box");
            var objBigBox = document.getElementById("big-box");
            var objBigBoxImage = objBigBox.getElementsByTagName("img")[0];

            objMark.onmouseover = function () {
                objFloatBox.style.display = "block"
                objBigBox.style.display = "block"
            }

            objMark.onmouseout = function () {
                objFloatBox.style.display = "none"
                objBigBox.style.display = "none"
            }

            objMark.onmousemove = function (ev) {

                var _event = ev || window.event;  //兼容多个浏览器的event参数模式

                var left = _event.clientX - objDemo.offsetLeft - objSmallBox.offsetLeft - objFloatBox.offsetWidth / 2;
                var top = _event.clientY - objDemo.offsetTop - objSmallBox.offsetTop - objFloatBox.offsetHeight / 2;

                if (left < 0) {
                    left = 0;
                } else if (left > (objMark.offsetWidth - objFloatBox.offsetWidth)) {
                    left = objMark.offsetWidth - objFloatBox.offsetWidth;
                }

                if (top < 0) {
                    top = 0;
                } else if (top > (objMark.offsetHeight - objFloatBox.offsetHeight)) {
                    top = objMark.offsetHeight - objFloatBox.offsetHeight;

                }

                objFloatBox.style.left = left + "px";   //oSmall.offsetLeft的值是相对什么而言
                objFloatBox.style.top = top + "px";

                var percentX = left / (objMark.offsetWidth - objFloatBox.offsetWidth);
                var percentY = top / (objMark.offsetHeight - objFloatBox.offsetHeight);

                objBigBoxImage.style.left = -percentX * (objBigBoxImage.offsetWidth - objBigBox.offsetWidth) + "px";
                objBigBoxImage.style.top = -percentY * (objBigBoxImage.offsetHeight - objBigBox.offsetHeight) + "px";
            }
        }
    </script>
</head>
<body>
<div id="demo">
    <div id="small-box">
        <div id="mark"></div>
        <div id="float-box"></div>
        <img src="image/macbook-small.jpg"/>
    </div>
    <div id="big-box">
        <img src="image/macbook-big.jpg"/>
    </div>
</div>
</body>
</html>
```
**解决兼容性问题** 
测试工具：IETester
[详情讲解](http://www.imooc.com/video/419)

主要思路：加一个遮罩层

另附jQuery实现代码

```
 <!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>放大镜</title>
<script src="http://libs.baidu.com/jquery/1.10.0/jquery.min.js"></script>

<style type="text/css">
* {
margin: 0;
padding: 0
}

#demo {
display: block;
width: 400px;
height: 255px;
margin: 50px;
position: relative;
border: 1px solid #ccc;
}

#small-box {
position: relative;
z-index: 1;
}

#float-box {
display: none;
width: 160px;
height: 120px;
position: absolute;
background: #ffffcc;
border: 1px solid #ccc;
filter: alpha(opacity=50);
opacity: 0.5;
cursor: move;
}

#mark {
position: absolute;
display: block;
width: 400px;
height: 255px;
z-index: 10;
background: #fff;
filter: alpha(opacity=0);
opacity: 0;
cursor: move;
}

#big-box {
display: none;
position: absolute;
top: 0;
left: 460px;
width: 400px;
height: 300px;
overflow: hidden;
border: 1px solid #ccc;
z-index: 1;;
}

#big-box img {
position: absolute;
z-index: 5
}
</style>
<script>
    $(function(){
        var markWidth = $('#mark').width(),
            markHeight = $('#mark').height(),
            floatBoxWidth = $('#float-box').width(),
            floatBoxHeight = $('#float-box').height(),
            percent = $('#big-box').width() / $('#float-box').width()
        $('#mark').on('mouseover', function(){
            $('#float-box').show()
            $('#big-box').show()
        }).on('mouseout', function(){
            $('#float-box').hide()
            $('#big-box').hide()
        }).on('mousemove', function(e){
            e = e || window.event
            var markOffset = $('#mark').offset()
            var left = e.clientX - markOffset.left - floatBoxWidth / 2,
                top = e.clientY - markOffset.top - floatBoxHeight / 2
            if(left < 0) left =0
            else if(left > markWidth - floatBoxWidth) left = markWidth - floatBoxWidth
            if(top < 0) top =0
            else if(top > markHeight - floatBoxHeight) top = markHeight - floatBoxHeight
            $('#float-box').css({left: left+'px', top: top+'px'})
            $('#big-box>img').css({left: -left*percent+'px', top: -top*percent+'px'})
        })
    })
</script>


</head>
<body>
<div id="demo">
<div id="small-box">
<div id="mark"></div>
<div id="float-box"></div>
<img src="image/macbook-small.jpg"/>
</div>
<div id="big-box">
<img src="image/macbook-big.jpg"/>
</div>
</div>
</body>
</html>
```

参考：
> [慕课网 用JS实现放大镜特效](http://www.imooc.com/learn/32)