---
layout: post
title: 一步一步学习css
summary: |
 大白源码转载于：<a href="http://www.w3cfuns.com/home.php?mod=space&uid=5455933&do=index">wocacaca的博客</a><br />
 大白原文链接：<a href="http://www.w3cfuns.com/blog-5455933-5404334.html">自己写的css3大白机器人~</a>
 <p>
 <h2>什么是CSS？</h2>

 CSS - Cascading Style Sheets：中文译名即“层叠样式表”，它可以用来定义页面样式，精准控制页面布局。它可以在不更改原HTML代码的前提下，通过链接不同的css文件来更换整个页面风格。
 </p>
author: xenonchau
category: tutorial
tag:
- WebSite
---

<style type="text/css">
 .header h1 {
 	color: red;
 }
</style>

##什么是CSS？

CSS - Cascading Style Sheets：中文译名即“层叠样式表”，它可以用来定义页面样式，精准控制页面布局。它可以在不更改原HTML代码的前提下，通过链接不同的css文件来更换整个页面风格。
<hr />

##如何来写一条css？

我们写文章通常都要先写“标题”，那么我们来更改一下HTML里的“Heading 1”&lt;h1&gt;Hello  World&lt;/h1&gt;的颜色，来作为第一条css代码的范例吧。
{% highlight html %}
<!-- 在<head></head>内添加如下代码 -->
<style type="text/css"> /*这里声明内部代码是css*/
	.header h1 { /*这里声明了一个控制域名称，前面用“.”来说明。*/
		color: red; /*颜色可以用英文、RGB颜色表rgb(255,255,255)或者十六进制数字#FFFFFF来声明。*/
	}
</style>
<!--在<body></body>中，<div>内用class属性调用之前声明的定义域即可。-->
<div class='header'> <!--<div>标签内调用的是之前.header内声明的样式。-->
	<h1>Hello World</h1>
</div>
{% endhighlight %}

<br />

> <div class='header'> 
> 	<h1>Hello World</h1>
> </div>
>
> 如何？看到效果了吧？
> 同理，段落标签&lt;p&gt;&lt;/p&gt;、超链接标签&lt;a&gt;&lt;/a&gt;等等全部都可以定义，如果想要在不同位置定义不同的样式，只需要增加另外一个定义域名称就可以了。eg: .body h1

<hr />

##有没有更多功能呢？

当然有了，因为我也是在一步一步的从零学起，所以推荐诸位看官一个学习网站：[Code Cademy](http://www.codecademy.com/)。这里的教学方式就是由浅入深循序渐进的，而且每操作一步都能实时反馈最终效果。

<hr />

最后给大家演示一下来自[前端网](http://www.w3cfuns.com/)的一位同学：[wocacaca](http://www.w3cfuns.com/home.php?mod=space&do=blog&uid=5455933&from=space)的作品：[自己写的css3大白机器人~](http://www.w3cfuns.com/blog-5455933-5404334.html)

> [Baymax - Big Hero 6](http://www.xenonchau.com/baymax.html)<br />
> ![baymax](http://www.xenonchau.com/images/2015-03-25-baymax.png)










