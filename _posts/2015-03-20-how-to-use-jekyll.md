---
layout: post
title: 使用Jekyll搭建一个博客 (一)
summary: 如何搭建本地环境
category: tutorial
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
![](images/2015-03-20-0000.jpeg)

项目名称一定要和自己的用户名一致，<br>
这是Github为方便访问web托管项目约定好的一种格式。<br>
把图片中的<code>yourname</code>换成你的用户名。<br>
![](/images/2015-03-20-0001.jpeg)<br>
如果想要<code>clone</code>你的项目到本地，把图片下方未勾选的<code>Initialize this repository with a README</code>
然后点击<code>Create Repository</code>。

**这样基本工作就做好了。**
<hr>
####搭建本地环境
检查一下本机是否已经安装了ruby，如果已安装则跳过这一步。<br>
<code>Windows环境</code><br>
略<br>

<code>Mac环境</code><br>
打开Terminal，依次检查ruby、gem和git版本。
{% highlight bash lineno %}
$ ruby --version
ruby 2.0.0p481 (2014-05-08 revision 45883) [universal.x86_64-darwin13]
{% endhighlight %}
{% highlight bash lineno %}
$ gem --version
2.4.6
{% endhighlight %}
{% highlight bash lineno %}
$ git --version
git version 1.9.5 (Apple Git-50.3)
{% endhighlight %}
如果没有安装git，可以参考[［廖雪峰］](http://www.liaoxuefeng.com/ "廖雪峰，十年软件开发经验，业余产品经理，精通Java/Python/Ruby/Visual Basic/Objective C等，对开源框架有深入研究，著有《Spring 2.0核心技术与最佳实践》一书，多个业余开源项目托管在GitHub。"")的文章：[［安装Git］](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000)<br>
Mac系统预装了ruby，所以只需要检查一下版本是否>=1.9.4即可。

然后就该安装Jekyll了<br>
由于gem源被墙了，未翻墙的同学可以把gem源换成淘宝的源。
{% highlight bash lineno %}
$ gem sources --remove http://rubygems.org/  
$ gem sources -a http://ruby.taobao.org/  
$ gem sources -l 
# 请确保只有 ruby.taobao.org，如果不移除rubygems.org，安装会非常慢。
{% endhighlight %}
之后就可以进行安装了。<br>
{% highlight bash lineno %}
$ sudo gem install jekyll -V
# 加入sudo，不然中间会出现Library文件夹没有权限写入的错误。
# -V 大写的V可以显示详细信息。
{% endhighlight %}
时间不长，稍等一下，喝杯咖啡、刷刷Weibo……

**至此本地环境安装完毕。**
<hr>
####把Github上的项目复制到本机

如果你按照上面[廖雪峰 - 安装Git](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000)的教程做了，<br>
那你一定已经设置过Git了。
{% highlight bash lineno %}
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
# 因为Git是分布式版本控制系统，
# 所以，每个机器都必须自报家门：你的名字和Email地址。
# 你也许会担心，如果有人故意冒充别人怎么办？
# 这个不必担心，首先我们相信大家都是善良无知的群众，
# 其次，真的有冒充的也是有办法可查的。
# 注意git config命令的--global参数，
# 用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，
# 当然也可以对某个仓库指定不同的用户名和Email地址。
{% endhighlight %}
这个时候就可以把刚刚的在Github上创建的项目<code>clone</code>到本地了。<br>
在你的项目目录下，复制你的clone链接。<br>
![](/images/2015-03-20-0002.jpeg)

在Terminal中输入：
{% highlight bash lineno %}
$ git clone https://github.com/yourname/yourname.github.io.git
Cloning into 'yourname.github.io'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done.
{% endhighlight %}
这个时候我们就已经把Git仓库里的项目<code>clone</code>到本机了，<br>
我们进入文件夹看看成功与否：
{% highlight bash lineanchors %}
$ cd yourname.github.io
$ ls
README.md
{% endhighlight %}
显示README.md已经从远程仓库<code>clone</code>到本机了。

**至此，本地仓库建立完成。**
<hr>
###写入一个页面
**要创建一个博客有两种方法：**

***在网上选择一个好看的模板***<br>
在这里分享几个链接：<br>
[Jekyll Themes](http://jekyllthemes.org/)<br>
[Jekyll Themes - Themes and templates for the Jekyll static site generator.](http://www.jekyllthemes.net/)<br>
[Themes - 掌心](http://www.zhanxin.info/themes.html)<br>
<code>Download zip</code>或者<code>clone</code>到本机。

***自己搭建一个Jekyll框架***<br>
首先我们要了解一下Jekyll Blog的目录结构：
{% highlight Bash shell scripts %}
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
│   └── 2013-08-07-welcome-to-jekyll.markdown
├── _site
└── index.html
{% endhighlight %}
| 文件/目录 | 描述 |
|:--------|:--------|
| <code>_config.yml</code> | 存储配置数据。很多全局的配置或者指令写在这里。 |
| <code>_drafts</code> | 存放为发表的文章。这些是没有日期的文件。 |
| <code>_includes</code> | 存放一些页面组件。可以通过&#123;&#37; include file.ext &#37;&#125; 来引用。|
| <code>_layouts</code> | 页面布局，也就是模板。 |
| <code>_posts</code> | 存放写文章，格式化为：YEAR-MONTH-DAY-title.md。 |
| <code>_site</code> | 最终生成的blog网站就在这里。 |
| <code>index.html</code> | 博客的主页。 |
| <code>_assets</code> | 我们还可以添加一个文件夹，用来存放图片,css样式表等资源。 |

只要我们把写好的博文放到<code>_post</code>目录下，通过<code>jekyll build</code>，该目录就会被复制到<code>_site</code>里面。

原理我们都明白了，那么就开始实战来检验理论吧？

下集：[《如何使用Jekyll搭建一个博客 (二) － 如何发布一篇博文》](tutorial/2015/03/20/how-to-post-a-blog.html)

