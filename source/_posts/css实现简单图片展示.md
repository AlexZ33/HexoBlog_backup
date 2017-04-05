---
title: CSS实现简单图片展示
date: 2016-03-07 18:44:12
tags:
- CSS
- 网站常用特效
- 图片展示
- 商品展示
- 日志
- 前端
categories: 前端
---
<b>CSS实现简单图片展示<b>

  **效果：**
  ![](http://on891bjlf.bkt.clouddn.com/gif/picshow.gif)
  
css部分
```css
  
div,ul,li,dl,dt,dd{
	margin:0;
	padding:0;
}
ul,li,dl,dt,dd{
	list-style:none;
}
.demo{
	margin:0 auto;
	width:930px;
}
.demo ul li{
	float:left;
	width:300px;
	margin-right:6px;
	position:relative;
}
.demo ul li img{
    border:none;
	position:relative;
	z-index:22;
}
.demo ul li a{
	width:300px;
    display:block;
	border:2px solid #ccc;
}
.demo ul li a:hover{
	border:2px solid #C03;
}

.demo ul li a span{
    position:absolute;
	z-index:33;
	bottom:2px;
	left:2px;
	width:300px;
	height:40px;
	filter:alpha(Opacity=50);
	-moz-opacity:0.5;
	opacity: 0.5;
	background:#000;
	color:#fff;
	line-height:40px;
	text-align:left;
	display:none;
}
.demo ul li a:hover span{
	display:block;
}
    
```

html部分

    <div class="demo">
    <ul>
       <li>
         <a>
           <img src="1.jpg"  />
           <span>keep moving</span>
         </a>
       </li>
       <li>
         <a>
           <img src="2.jpg"  />
           <span>stay hungry </span>
         </a>
       </li>
       <li>
         <a>
           <img src="3.jpg"  />
           <span>stay foolish</span>
         </a>
       </li>
    </ul>
 </div>

**参考**
[慕课网 图片展示特效](http://www.imooc.com/learn/31)