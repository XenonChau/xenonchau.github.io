---
layout: post
title: 如何使用Jekyll搭建一个博客
summary: 如何使用Jekyll搭建一个博客
category: 技术文章
tags:
- WebSite
---

####First of all
首先我们要注册一个Github账号。[点击这里注册](https://github.com/join)<br>
这里用来存放你的网页，完全免费。<br>
{%highlight ruby%}
# 注册大家都会，我就不啰嗦了。
{%endhighlight%}

<br>
<hr>
####建立项目
在Github的右上角<code>Add New Repository</code><br>
<img src="/images/2015-03-20-0000.jpeg">

项目名称一定要和自己的用户名一致，<br>
这是Github为方便访问web托管项目约定好的一种格式。<br>
把图片中的<code>yourname</code>换成你的用户名。<br>
<img src="/images/2015-03-20-0001.jpeg"><br>
然后点击<code>Create Repository</code>。<br>
这样基本工作就做好了。
<hr>
####搭建本地环境
检查一下本机是否已经安装了ruby，如果已安装则跳过这一步。<br>
<code>Windows环境</code><br>
略<br>

<code>Mac环境</code><br>
打开Terminal，依次检查ruby、gem版本。
{% highlight ruby %}
$ ruby --version
ruby 2.0.0p481 (2014-05-08 revision 45883) [universal.x86_64-darwin13]
{% endhighlight %}
{% highlight ruby %}
$ gem --version
2.4.6
{% endhighlight %}
Mac系统预装了ruby，所以只需要检查一下版本是否>=1.9.4即可。

然后就该安装Jekyll了<br>
由于gem源被墙了，未翻墙的同学可以把gem源换成淘宝的源。
{% highlight ruby %}
$ gem sources --remove http://rubygems.org/  
$ gem sources -a http://ruby.taobao.org/  
$ gem sources -l 
# 请确保只有 ruby.taobao.org，如果不移除rubygems.org，安装会非常慢。
{% endhighlight %}
之后就可以进行安装了。<br>
{% highlight ruby %}
$ sudo gem install jekyll -V
# 加入sudo，不然中间会出现Library文件夹没有权限写入的错误。
# -V 大写的V可以显示详细信息。
{% endhighlight %}
时间不长，稍等一下，喝杯咖啡、刷刷Weibo……<br>
至此本地环境安装完毕。




**Method 1.** In [index.html](https://github.com/yulijia/freshman21/blob/master/index.html) file, set <code> \{\{ post.content | strip_html | truncatewords: 50 \}\}</code> , produces a more consistent excerpt. It gets the first 50 words and strips any formatting.

This method can automatically create a summary of article. However if the article begin with <q>code</q> or <q>markdown tags</q>, you will find the article css style can not shown on the home page.

**Method 2.** In [index.html](https://github.com/yulijia/freshman21/blob/master/index.html) file, using <code>\{\{ post.summary \}\}</code> to insted of <code>\{\{ post.content \}\}</code>, produces a summary of post. You need add summary in each <q>post</q> file, [example](https://gist.github.com/yulijia/2f865b78a28bfe9e0a81#file-a-article-post-with-summary)

Then you will find all articles summary in the home page.




### How to create a read more button for a post? 


Basically, freshman21 doesn't support "read more" button.

To create a page link(button) is very easy.

Just add 
{% highlight HTML%}
 <p><a href="\{\{ post.url | prepend: site.baseurl \}\}">read more</a></p> 
{% endhighlight %}

after <code>\{\{post.summary\}\}</code>

## The example of post summary at [Gist](https://gist.github.com/yulijia/2f865b78a28bfe9e0a81).

-----

## you can clone the readmore version by using

<code>git clone --branch readmore https://github.com/yulijia/freshman21.git</code>