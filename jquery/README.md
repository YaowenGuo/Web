轻量级javascript库，不仅兼容css3，还兼容各种浏览器
目标：写的更少，做的更多，不用程序员自己再去做适配

优点：
容易上手
强大的选择器
解决浏览器的兼容
完善的事件机制
出色的Ajax封装
丰富的UI

特性：
链式操作
回调函数
迭代器
延迟对象
队列

## 环境搭建
进入官方网站获取最新的版本 http://jquery.com/download/  ，这里需要注意 jQuery 分 2 个系列版本 1.x 与 2.x，主要的区别在于 2.x 不再兼容 IE6、7、8浏览器，这样做的目的是为了兼容移动端开发。由于减少了一些代码，使得该版本比 jQuery 1.x 更小、更快。

如果开发者比较在意老版本 IE 用户，只能使用 jQuery 1.9 及之前的版本了。我们这本课程为了兼容性问题，使用的是 1.9 版本。jQuery 每一个系列版本分为：压缩版(compressed) 与 开发版(development)，我们在开发过程中使用开发版（开发版本便于代码修改及调试），项目上线发布使用压缩版（因为压缩版本体积更小，效率更快）。

 jQuery是一个JavaScript脚本库，不需要特别的安装，只需要我们在页面 <head> 标签内中，通过 script 标签引入 jQuery 库即可。
```
<!DOCTYPE HTML>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <script type="text/javascript" src="https://www.imooc.com/static/lib/jquery/1.9.1/jquery.js"></script>
    <title>环境搭建</title>
</head> 
<body>
    <script type="text/javascript"> alert($) </script>
</body>
</html>
```

alert 弹出以上信息，说明环境已经搭建成功了。


## Hello Word
```
<script type="text/javascript">
            $(document).ready(function() {
                    $("div").html("Hello Word!");
            });
</script>
```
代码分析：
$(document).ready 的作用是等页面的文档（document）中的节点都加载完毕后，再执行后续的代码，因为我们在执行代码的时候，可能会依赖页面的某一个元素，我们要确保这个元素真正的的被加载完毕后才能正确的使用。