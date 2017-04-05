---
title: CSS3实现三角形和气泡效果
date: 2016-01-07 18:44:12
tags:
- CSS3
- 三角形
- 气泡效果
- 前端
- 日志
categories: 前端
---
<b>三角形的实现<b>


html结构
```html
        <body>
        	<div></div>
        </body>
```
css样式
```css3
        div{
			height: 0;
			width: 0;
			border-top: 40px solid #000;
			border-right: 40px solid #ff0000;
			border-left: 40px solid #ff0000;
			border-bottom: 40px solid #000;
		}
```

显示效果
![显示效果](http://on891bjlf.bkt.clouddn.com/mage/css3/%E6%88%AA%E5%9B%BE1490612265.png)
用css画三角形很简单，就是将一个块元素宽高设置为0，然后给某一边设一个比较厚的宽度
利用盒子的均分原理，盒子都是矩形或者正方形，从形状的中心，向4个
上下左右划分4个部分。保证元素是块级元素，设置元素的边框，不需要显示的边框使用透明色transparent。

所以，如果你要一个向上或者向下的三角:border-left和border-right就是transparent，而border-bottom可见则三角向上，border-top可见则三角向下
```css3
       div{
				height: 0;
				width: 0;
				border-top: 40px solid transparent;
				border-right: 40px solid transparent;
				border-left: 40px solid transparent;
				border-bottom: 40px solid #000;
			}
```
![显示效果](http://on891bjlf.bkt.clouddn.com/mage/css3/%E6%88%AA%E5%9B%BE1490612957.png)
如果你要一个向左或者向右的三角:border-top和border-bottom就是transparent，而设置border-left则三角向右，设置border-right则三角向左
```css3
       div{
				height: 0;
				width: 0;
				border-top: 40px solid transparent;
				border-right: 40px solid transparent;
				border-left: 40px solid #000;
				border-bottom: 40px solid transparent;
			}
		
```
![显示效果](http://on891bjlf.bkt.clouddn.com/mage/css3/%E6%88%AA%E5%9B%BE1490613205.png)

如果它的上是有的，但是右是透明的，就会是下面的效果
border-top: 100px solid red;
border-right: 100px solid transparent;

```css3
      div{
				height: 0;
				width: 0;
				border-top: 40px solid #000;
				border-right: 40px solid transparent;
				
			}
		
		
```
![](http://on891bjlf.bkt.clouddn.com/mage/css3/%E6%88%AA%E5%9B%BE1490613452.png)

当然还有这样的：
```css3
     div{
				height: 0;
				width: 0;
				border-top: 40px solid #000;
				border-right: 30px solid #ff0000;
				border-left: 50px solid #ff0000;
				border-bottom: 25px solid #000;
	
			}
					
```
![](http://on891bjlf.bkt.clouddn.com/mage/css3/%E6%88%AA%E5%9B%BE1490613733.png)
很明显的左三角和下三角的比例是2:1，在下三角可以明显的看出来，下三角的底边，左右2:1；
同理，根据上面的上下左右布局，应该没有什么三角是画不出来的

示例 

如下图的时光轴旁边的小三角  就可以用以上的方法实现
```css3
    .content_item_icon_arrow{
				position: absolute;
				left: -10px;
				top: 20px;
				height: 0px;
				border-color:transparent #e2e2e2 transparent transparent;
				border-width: 10px 10px 10px 0px;
				border-style: dashed solid dashed dashed;

			}
					
```

<b>气泡效果实现<b>
 > 以前我们要实现对话气泡效果很麻烦，基本上是用切图的方法。现在有了CSS3就变得简单多了。一个HTML元素，一些CSS3代码，不需要图片，也不需要JavaScript。如下图：

 ```html
    <!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>	css3实现气泡</title>
	<style>
			.box{
				width: 200px;height: 100px; border: 5px solid #eee;margin-left: 10px;position: relative;
			}
			.box .arrow{
				position: absolute;top: 100px;left: 30px;width: 50px;height: 50px;
			}
			.a1{
				border: 30px solid #f00;display: block;border-color: #eee transparent transparent transparent;
			}
			.a2{position: absolute;left: 0;top: -8px;border: 30px solid #f00;display: block;border-color: #fff transparent transparent transparent }
		
	</style>
</head>
<body>
	<div class="box">
		<div class="arrow">
			<span class="a1"></span>
			<span class="a2"></span>
		</div>
		<p>
			css3实现气泡
		</p>
	</div>
</body>
</html>
					
```
效果
![](http://on891bjlf.bkt.clouddn.com/mage/css3/%E6%88%AA%E5%9B%BE1490616586.png)

```html
<!DOCTYPE html>
<html>
<head>
<title></title>
</head>
<style type="text/css">
#demo{
    position: relative;
    width: 200px;
    height: 100px;
    background-color: #fff;
    border: 8px solid #666;
    -webkit-border-radius: 30px;
    -moz-border-radius: 30px;
    border-radius: 30px;
    -webkit-box-shadow: 2px 2px 4px #888;
    -moz-box-shadow: 2px 2px 4px #888;
    box-shadow: 2px 2px 4px #888;
}
#demo:before{
    content: ' ';
    position: absolute;
    width: 0;
    height: 0;
    left: 30px;
    top: 100px;
    border: 25px solid;
    border-color: #666 transparent transparent #666;
}
#demo:after{
    content: ' ';
    position: absolute;
    width: 0;
    height: 0;
    left: 38px;
    top: 100px;
    border: 15px solid;
    border-color: #fff transparent transparent #fff;
}
</style>
<body>
    <div id="demo"></div>
</body>
</html>
```
效果：
![](http://on891bjlf.bkt.clouddn.com/mage/css3/%E6%88%AA%E5%9B%BE1490616951.png)

> 参考：
> [CSS3实现气泡效果](https://segmentfault.com/a/1190000000479199)
> [CSS3 巧妙实现聊天气泡](https://segmentfault.com/a/1190000007159738)
> [CSS3 聊天气泡框以及 inherit、currentColor 关键字](https://segmentfault.com/a/1190000006023203)