---
title: '主题butterfly如何让你的博客拥有星空背景和流星特效'
date: 2023-02-19 16:10:50
tags: [美化]
published: true
hideInList: false
feature: 
isTop: false
---
切换夜间暗黑模式后主题显示星空特效，并且还有流星
<!-- more -->

最近很多小伙伴留言想要星空和流星特效，于是写了这篇文章准备介绍如何部署。

# 创建js文件

1. 插入Canvas标签
  首先打开Butterfly主题的`_config.yml`文件或者使用HTML直接插入，找到配置文件对应的`inject`部分

  插入`<canvas id="universe"></canvas>`

2. 创建JS文件
  在`butterfly/source/js/`创建一个`universe.js`文件，或者添加到自己的js文件中

~~~js
function dark() {window.requestAnimationFrame=window.requestAnimationFrame||window.mozRequestAnimationFrame||window.webkitRequestAnimationFrame||window.msRequestAnimationFrame;var n,e,i,h,t=.05,s=document.getElementById("universe"),o=!0,a="180,184,240",r="226,225,142",d="226,225,224",c=[];function f(){n=window.innerWidth,e=window.innerHeight,i=.216*n,s.setAttribute("width",n),s.setAttribute("height",e)}function u(){h.clearRect(0,0,n,e);for(var t=c.length,i=0;i<t;i++){var s=c[i];s.move(),s.fadeIn(),s.fadeOut(),s.draw()}}function y(){this.reset=function(){this.giant=m(3),this.comet=!this.giant&&!o&&m(10),this.x=l(0,n-10),this.y=l(0,e),this.r=l(1.1,2.6),this.dx=l(t,6*t)+(this.comet+1-1)*t*l(50,120)+2*t,this.dy=-l(t,6*t)-(this.comet+1-1)*t*l(50,120),this.fadingOut=null,this.fadingIn=!0,this.opacity=0,this.opacityTresh=l(.2,1-.4*(this.comet+1-1)),this.do=l(5e-4,.002)+.001*(this.comet+1-1)},this.fadeIn=function(){this.fadingIn&&(this.fadingIn=!(this.opacity>this.opacityTresh),this.opacity+=this.do)},this.fadeOut=function(){this.fadingOut&&(this.fadingOut=!(this.opacity<0),this.opacity-=this.do/2,(this.x>n||this.y<0)&&(this.fadingOut=!1,this.reset()))},this.draw=function(){if(h.beginPath(),this.giant)h.fillStyle="rgba("+a+","+this.opacity+")",h.arc(this.x,this.y,2,0,2*Math.PI,!1);else if(this.comet){h.fillStyle="rgba("+d+","+this.opacity+")",h.arc(this.x,this.y,1.5,0,2*Math.PI,!1);for(var t=0;t<30;t++)h.fillStyle="rgba("+d+","+(this.opacity-this.opacity/20*t)+")",h.rect(this.x-this.dx/4*t,this.y-this.dy/4*t-2,2,2),h.fill()}else h.fillStyle="rgba("+r+","+this.opacity+")",h.rect(this.x,this.y,this.r,this.r);h.closePath(),h.fill()},this.move=function(){this.x+=this.dx,this.y+=this.dy,!1===this.fadingOut&&this.reset(),(this.x>n-n/4||this.y<0)&&(this.fadingOut=!0)},setTimeout(function(){o=!1},50)}function m(t){return Math.floor(1e3*Math.random())+1<10*t}function l(t,i){return Math.random()*(i-t)+t}f(),window.addEventListener("resize",f,!1),function(){h=s.getContext("2d");for(var t=0;t<i;t++)c[t]=new y,c[t].reset();u()}(),function t(){document.getElementsByTagName('html')[0].getAttribute('data-theme')=='dark'&&u(),window.requestAnimationFrame(t)}()};
dark()

~~~

代码最后这一部分要求**data-theme**也就是主题为**dark**暗色主题，因此仅在暗色主题生效，随后将**js**文件添加到配置文件的inject处或者其他需要的位置。

# 创建css文件

1. CSS样式 在 `[BlogRoot]/source/css` 目录下新建 `universe.css`，输入以下代码：

~~~css
/* 背景宇宙星光  */
#universe{
  display: block;
  position: fixed;
  margin: 0;
  padding: 0;
  border: 0;
  outline: 0;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: -1;
}

~~~
# 引入文件
1. 在主题配置文件`_config.butterfly.yml` 的 `inject` 配置项中 `bottom` 下填入：

~~~ymd
inject:
  bottom:
   - <canvas id="universe"></canvas>
   - <script defer src="/js/universe.js"></script>
~~~

2. 在主题配置文件`_config.butterfly.yml` 的 `inject` 配置项中 `head` 下填入：

~~~ymd
inject:
  head:
   - <link rel="stylesheet" href="/css/universe.css">
~~~

本文部分转载于：[基于 Hexo 从零开始搭建个人博客（六）][1]


  [1]: http://%E5%9F%BA%E4%BA%8E%20Hexo%20%E4%BB%8E%E9%9B%B6%E5%BC%80%E5%A7%8B%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%EF%BC%88%E5%85%AD%EF%BC%89