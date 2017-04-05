---
title: canvas绘制闪烁星星效果
date: 2016-01-25 19:56:16
tags:
- canvas
- animation
- 动画
- 前端
- 轮播序列帧
categories: 前端
---
<b>canvas绘制闪烁星星效果<b>

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width=330 height=86 src="//music.163.com/outchain/player?type=2&id=1237111&auto=1&height=66"></iframe>
--------
GitHub：https://github.com/AlexZ33/canvas_demo/tree/gh-pages
[演示链接](http://jxdxsw.com/canvas_demo/twinkling_stars/twinkling_stars.html)  
![效果](http://on891bjlf.bkt.clouddn.com/gif/staring.gif)
-------
主要知识点
--------
- 如何轮播序列帧
- canvas API 
	- drawImage();
	- globalAlpha;
	- Save;
	- Restore
- 如何添加鼠标事件
- 循环调用 Window API  
	-requestAnimFrame(function(){});
	-setTimeout(function(){},time);
	-setInterval(function(){},time);
	三者的区别

总体思路
--------
- 搭建网页结构
- 绘制背景
- 绘制女孩图片
- 鼠标点画圆闪烁变动，以及连线其他原点
- requestAnimationFrame 更新画面

> 参考：
> [慕课网 canvas实现星星闪烁特效](http://www.imooc.com/learn/338)
> [GameLoop的几种实现方式](http://www.bennychen.cn/2011/06/game-loop-model/)
> [Javascript中的setTimeout,setInterval,requestAnimFrame](http://blog.csdn.net/pearyangyang/article/details/45561115)
> [Request Animation Frame for Better Performance]https://software.intel.com/en-us/html5/hub/blogs/request-animation-frame-for-better-performance/


