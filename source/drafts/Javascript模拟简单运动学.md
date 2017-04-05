
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <link rel="dns-prefetch" href="//www.google-analytics.com">
        <link rel="dns-prefetch" href="//static.hello13.net">

        <title>JavaScript模拟简单运动学</title>
        <meta name="generator" content="Jekyll" />
        <meta name="author" content="有田十三" />
        <meta name="description" content="" />
        <meta name="keywords" content="" />

        <!-- Mobile Specific Metas ================================================== -->

        <meta name="apple-mobile-web-app-capable" content="yes" />
        <meta name="apple-touch-fullscreen" content="yes">
        <meta name="apple-mobile-web-app-status-bar-style" content="black" />
        <meta name="format-detection" content="telephone=no" />
        <meta name="format-detection" content="email=no" />
        <meta name="format-detection" content="address=no" />

        <!-- Favicon.ico & App Links ================================================== -->
        <link rel="apple-touch-icon" sizes="120x120" href="/static/img/favicon/apple-icon-120x120.png">
        <link rel="icon" type="image/png" sizes="96x96" href="/static/img/favicon/favicon-96x96.png">

        
        <link rel="stylesheet" href="http://static.hello13.net/css/screen.min.css" media="screen, projection" />
        

        <script type="text/javascript">
            //根据屏幕大小及dpi调整缩放和大小
            (function() {
                var scale = 1.0;
                var ratio = 1;

                var ua = navigator.userAgent;
                var isChrome = ua.match(/Chrome\/([\d.]+)/) || ua.match(/CriOS\/([\d.]+)/);

                if (window.devicePixelRatio >= 2 && !isChrome) {
                    scale *= 0.5;
                    ratio *= 2;
                }
                var text = '<meta name="viewport" content="initial-scale=' + scale + ', maximum-scale=' + scale +', minimum-scale=' + scale + ', width=device-width, user-scalable=no" />';
                document.write(text);
                document.documentElement.style.fontSize = 50*ratio + "px";
            })();
        </script>

        <script>
            var requirejs = {
                __require: [],
                __requirejsConfig: {
                
                    revision: {
  "page.js": "033a5aab",
  "com/album.js": "731e8349",
  "com/test.js": "15637546",
  "com/unveil.js": "f031d2f5",
  "lib/fastclick.js": "6e9d3b0d",
  "lib/truck.js": "873b2929",
  "lib/zepto.js": "7b14eb05",
  "util/autocomp.js": "c4d8ce84",
  "util/box.js": "5ac874d0",
  "util/dip.js": "6aadf593",
  "util/hidebar.js": "718a15e6",
  "util/url.js": "9e507c7b",
  "util/act/fft.js": "a82ccd7c",
  "util/act/gesture.js": "0f975d71",
  "util/act/matrix.js": "478dd6b7",
  "util/act/page.js": "1e595416",
  "util/act/pageable.js": "9fb71634"
},
                    combo: {
                        url: 'http://static.hello13.net/combo?f='
                    },
                    prefix: '/js/'
                
                }
            }, require = function() {
                requirejs.__require.push(arguments);
            };
        </script>
    </head>
    <body>
        <header>
            <nav>
                <div class="slogan"><a href="/">Hello13</a></div>
                <div class="menu">
                    <span class="menu-icon" id='menu'></span>
                    <div class="menu-list">
                        <dl><a href="/home/">Home</a></dl>
                        <dl><a href="/posts/">Posts</a></dl>
                        <dl><a href="/projects/">Projects</a></dl>
                        <dl><a href="/posts/me/">About Me</a></dl>
                    </div>
                </div>
            </nav>
        </header>
        <section>
            <article>
                <div class="content markdown-body">
    <h1>JavaScript模拟简单运动学</h1>
    <p class="meta">02 Mar 2014 - Sysu, Guangzhou</p>
    <style>
    #container {
        background: rgba(0,0,0,0.6);
        border: 1px solid #fff;
        position: relative;
        width: 600px;
        height: 300px;
    }
    #move {
        position: absolute;
        background: #fff;
        width: 10px;
        height: 10px;
        border-radius: 50% 50%;
    }
</style>

<div id="container">
    <div id="move" style="left:0px;top:0px"></div>
</div>
<button id='g_btn'>Click</button>
<p>我是一个占位符，文章等等慢慢补。</p>
<script>
    var $$ = function(id) { return document.getElementById(id); }
    var drop = function () {
        var conEl = $$("container"),
            moveEl = $$("move"),
            maxDis = (conEl.offsetHeight - parseInt(moveEl.style.height)) || (300 - 10),
            nowTop, nowLeft, topDis, stepDis = 1, direction = "down";

        // 恢复初始状态
        moveEl.style.top = 0 + 'px';
        moveEl.style.left = 0 + 'px';

        var moveTimer = setInterval(function(){

            nowTop = parseInt(moveEl.style.top);
            nowLeft = parseInt(moveEl.style.left);

            nowLeft += 1;
            switch(direction) {
                case "up": moveUp(); break;
                case "down": moveDown(); break;
            }
            function moveDown(){
                nowTop += stepDis * 0.05;
                stepDis += 2;
                if( nowTop > maxDis ){
                    direction = "up";
                }
            }
            function moveUp(){
                nowTop -= stepDis * 0.05 / 2;
                stepDis -= 2;
                if( nowTop <= 0 || stepDis < 0 ){
                    direction = "down";
                }
            }
            if( nowLeft > 590 ){
                clearInterval(moveTimer);
                g_btn.removeAttribute("disabled");
                return;
            }
            moveEl.style.top = nowTop + 'px';
            moveEl.style.left = nowLeft + 'px';
        },10);
    }
    var g_btn = $$('g_btn');
    g_btn.onclick = function(){
        drop();
        this.disabled = "disabled";
    }
</script>
</div>

<div class="related">
    <h2>Related Posts</h2>
    <ul class="posts">
    
        <li class="text-ellipsis">
            <span>09 Dec 2015</span> &raquo; <a href="/posts/router/">Router Middleware For Koa</a>
        </li>
    
        <li class="text-ellipsis">
            <span>25 Nov 2015</span> &raquo; <a href="/posts/localstorage/">Front-End Engineering：Cache Management</a>
        </li>
    
        <li class="text-ellipsis">
            <span>23 Nov 2015</span> &raquo; <a href="/posts/yahoo/">Best Practices For Speeding Up Your Web Site</a>
        </li>
    
    </ul>
</div>
            </article>
            <footer>
                <div class="contact">
                    <p>
                        Copyright  @有田十三<br />
                        Geek  of  <a href="http://github.com/">GitHub</a><br />
                        yooungt13@gmail.com
                    </p>
                </div><!--
             --><div class="contact">
                    <p>
                        <a href="http://weibo.com/yooungt/">weibo.com/yooungt</a><br />
                        <a href="http://github.com/yooungt13/">github.com/yooungt13</a><br />
                        <a href="http://blog.csdn.net/yooungt13/">blog.csdn.net/yooungt13</a>
                    </p>
                </div>
            </footer>
        </section>

        <script>
            require(['page.js'], function(page) {
                page.init();
            });
        </script>
        <script src="http://static.hello13.net/js/lib/truck.c4d5192a.js" async></script>
        <!--*********************************************************-->
        <!--******************Copyright @有田十三**********************-->
        <!--*********************************************************-->
    </body>
</html>


> **参考**
> [javascript模拟简单运动学](http://hello13.net/tags/datastructure/)