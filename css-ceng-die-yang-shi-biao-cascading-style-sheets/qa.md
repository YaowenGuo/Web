# 几种解决position:fixed 抖动的方法
http://blog.csdn.net/zx_001/article/details/50293709

原创 2015年12月14日 14:19:49 标签：css position 9152
最近在给客户做的手机版网站中用到了position:fixed 来模拟手机APP的底部的导航条，但是在三星手机的浏览器上出现了 抖动的情况，类似于下图这种情况：



 

在下滑的过程中，底部导航条会跟不上，在其它手机的浏览器里均没有这种情况

这种情况在IE6浏览器下也会出现。



经过查阅资料，总结出以下几种方法解决：

一.给fiexd加上如下CSS样式：

-webkit-transform: translateZ(0);

二.设置body CSS

html,
 body {height:100%;overflow:auto;margin: 0;}

这种方式可能会影响到页面的整体效果，不建议使用

三.在fiexd内设置position:absolute，如下：

<div style="position:fiexd;bottom:0px;">

  <div style="position:absolute;">

----

</div>

</div>


# CSS实现div内文字显示两行，超出两行部分省略号显示
https://www.cnblogs.com/zpsong/p/5406494.html

在搭建前台文章列表中，需要实现div内文字显示两行，超出的则省略号显示。

找了很多，都貌似只能一行显示。最后在百度知道找到答案。

答案转自百度知道，题主的自答。

用的是-webkit-私有属性。
text-overflow: -o-ellipsis-lastline;
overflow: hidden;
text-overflow: ellipsis;
display: -webkit-box;
-webkit-line-clamp: 2;
-webkit-box-orient: vertical;

另有回答是通过jquery来实现的
下载Jquery插件：jQuery ellipsis plugin
调用方法：
$(document).ready(function() {
　　$('.ellipsis').ellipsis();
}
