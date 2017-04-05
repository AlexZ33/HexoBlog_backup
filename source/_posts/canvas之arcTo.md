---
title: canvas之arcTo
date: 2016-02-021 16:44:12
tags:
- canvas
- arcTo
- 前端
- 日志
categories: 前端
---
<b>canvas之arcTo<b>

canvas提供画圆弧有两种方法，一个是arc，另一个就是arcTo，arc挺简单的，这里就不再说了，单说一下arcTo。
arcTo的作用是绘制介于两条切线之间的弧，语法是arcTo（x1,y1,x2,y2,r）,其中x1，y1是起始点的坐标，x2，y2是终点的坐标，r则是圆弧的半径。这里面有个很大的误区，一般的初学者看到这里，都会错误的判断起始点的位置，如图1所示：
![](http://on891bjlf.bkt.clouddn.com/canvas/%E9%94%99%E8%AF%AF.png)
![](http://on891bjlf.bkt.clouddn.com/canvas/%E6%AD%A3%E7%A1%AE.png)

正确的理解应如图2所示，起始点位于两条切线相交的位置，另外，终点也并不是弧的终点，而是另一条切线上的任意一点，拿图2来说，终点是竖直的那条切线上的一点。有人会问，可不可以在起始点的上面那里，因为切线是直线，可以延伸的。答案是当然可以，但这样的结果是圆弧就会向上弯曲，而不是向下弯曲了。
按我的理解，可以总结为，起始点控制前半段弧的方向，终点控制后半段弧的方向，至于r嘛，控制弧的大小。

下面一个简单的动画帮助理解
![](http://on891bjlf.bkt.clouddn.com/gif/arcTo.gif)

````
<!DOCTYPE html>  
<html>  
<head>  
<meta charset="UTF-8">  
<title>Insert title here</title>  
<style>  
canvas {  
    width: 400px;  
    height: 400px;  
    background-color: #EEEEEE;  
}  
</style>  
<script>  
    window.onload = function() {  
        var canvas = document.getElementById('canvas');  
        var arcToPoint1 = {x:120, y:40};  
        var arcToPoint2 = {x:60, y:80}  
        var context = canvas.getContext('2d');  
        if (!canvas || !canvas.getContext) {  
            return;  
        } else {  
            timer = setInterval(function(){  
                if (arcToPoint2.x < 150) {  
                    arcTo (context, arcToPoint1, arcToPoint2);  
                    arcToPoint2.x += 2;  
                } else {  
                    clearInterval(timer);  
                }  
            }, 300);  
        }  
    }  
      
    function arcTo () {  
        var startPoint = {x: 20, y: 40};  
        var context = arguments[0];  
        var arcToPoint1 = arguments[1];  
        var arcToPoint2 = arguments[2];  
        var context = canvas.getContext('2d');  
          
        context.clearRect(0,0,context.canvas.width, context.canvas.height)  
          
        context.beginPath();  
        context.moveTo(startPoint.x, startPoint.y);  
        context.strokeStyle = "red";  
        context.lineWidth = 1;  
        context.arcTo(arcToPoint1.x, arcToPoint1.y, arcToPoint2.x, arcToPoint2.y, 40);  
        context.stroke();  
          
        context.beginPath();  
        context.moveTo(startPoint.x, startPoint.y);  
        context.strokeStyle = "black";  
        context.lineWidth = 1;  
        context.lineTo(arcToPoint1.x, arcToPoint1.y);  
        context.fillText('arcToPoint1', arcToPoint1.x + 10, arcToPoint1.y - 5)   
        context.stroke();  
          
        context.beginPath();  
        context.moveTo(arcToPoint1.x, arcToPoint1.y);  
        context.strokeStyle = "black";  
        context.lineWidth = 1;  
        context.lineTo(arcToPoint2.x, arcToPoint2.y);  
        context.fillText('arcToPoint2', arcToPoint2.x + 10, arcToPoint2.y + 10)   
        context.stroke();  
    }  
</script>  
</head>  
<body>  
    <canvas id="canvas">  
        此游览器不支持canvas标签  
    </canvas>  
</body>  
</html>  
    
```
> **参考**
> [HTML5 canvas arcTo() 方法](http://www.w3school.com.cn/tags/canvas_arcto.asp)
> [Canavs arcTo方法的理解](http://blog.csdn.net/songzheng_741/article/details/26084829)