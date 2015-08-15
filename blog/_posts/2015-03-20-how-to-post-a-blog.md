---
layout: post
title: 使用Jekyll搭建一个博客 (二)
author: xenonchau 
summary: |
 <h3>如何发布一篇博文</h3>
 <p>首先我们要设置博客的全局变量：<code>_config.yml</code></p>
 <p>建立[_layout] [_post] [_include]文件夹</p>
 <p>在[_layout]文件夹中建立"post"模板</p>
 <p>建立一个用来展示[_post]文件夹中文章的主页<code>index.html</code></p>
category: tutorial
tags:
- WebSite
---


> 如果要手动写一个博客，我们需要有一点点<code>HTML</code>基础。

首先我们要设置博客的全局变量：<code>_config.yml</code><br>
{% highlight Bash shell scripts %}
### 站点信息：(Site info:)
title: # 你博客的名字
tagline: # 副标题，可以写点好听的座右铭。
author: # 默认作者，也就是你的名字。
email: # 你的电子邮件。
description: "some awesome words" # 描述文字，会出现在文档的head meta标签里，以及feed.xml里的站点描述里。
keywords: "keyword1, keyword2, keyword3" # 搜索引擎关键字。
baseurl: "blog" # 如果根目录就是博客，那这里就不填。
url: "http://www.YourSite.com" # 你网站的域名。


### 个人信息和组件信息：(Personal info and site tools info:)
twitter_username: #Twitter用户名
github_username:  #GitHub用户名
disqus_shortname: #Disqus用户名
favicon: "http://some-ico.ico" #显示在标签栏上的小图标。"16x16" ".ico"
aboutme: "these are shown on aboutme-sidebar." #短一点的个人简介，将会显示在侧边栏上。
aboutme_photo: "http://some-avatar.jpeg" # 你的头像。jpeg/jpg/png/bmp/...


### 站点设置：(Site setting:)
ShowContactInfo: "True" # aboutme栏里是否显示个人信息(twitter,github,email)：True/False
default_column: "two" # 博客风格: 双栏，如果default_column不是"two"，则显示一栏的博客样式。
default_locale: "cn" # 侧边栏语言设置，仅包含: 英文(en) 和 汉语 (cn)

locales: # 下面是默认语言的设置
    en:
      Aboutme: "About Me"
      Archives: "Archives"
      Blogroll: "Blogroll"
      Categories: "Categories"
      Copyright_Notice: "Copyright Notice"
      Recent_Posts: "Recent Posts"
      Tags: "Tags"
      Previous: "Older"
      Next: "Newer"
      PostedInCategories: "Posted in"
      Taggedwith: "and tagged"  
      PostDate: "on "
    cn:
      Aboutme: "关于我"
      Archives: "不是所有的鸡都叫时光鸡"
      Blogroll: "友情链接、共同创作者、特邀作者"        
      Categories: "分类目录"    
      Copyright_Notice: "版权声明"
      Recent_Posts: "近期文章"
      Tags: "标签" 
      Previous: "前一页"
      Next: "后一页"
      PostedInCategories: "目录:"   
      Taggedwith: "| 标签:"
      PostDate: "| 发表时间: "


### 网志提要信息，只在侧边栏显示名字。(your Blogroll info, only name can shown on the page.)

Blogroll:
    - name: 特邀作者的名字
      href: http://www.特邀作者的网站链接.com/
      title: 特邀作者的网站名称
    - name: 共同创作者的名字
      href: http://www.合作链接.com/
      title: 合作者网站的名字
    - name: 唐巧
      herf: http://blog.devtang.com/
      title: 唐巧的技术博客
    - name: 王巍
      herf: http://www.onevcat.com/
      title: OneV's Den


### 一些默认设置(Build settings)
markdown: kramdown # 默认markdown语言。
highlighter: pygments # 默认高亮语言。
paginate: 5 # 标页数。

# 来源：freshman21模板，更多用法请自行搜索。
{% endhighlight %}


> 为了能实时展现页面效果，我们用Jekyll开启一个本地服务器。

{% highlight Bash shell scripts %}
$ jekyll s
Configuration file: /Users/yourname/yourname.github.io/_config.yml
            Source: /Users/yourname/yourname.github.io
       Destination: /Users/yourname/yourname.github.io/_site
      Generating... 
                    done.
 Auto-regeneration: enabled for '/Users/yourname/yourname.github.io'
Configuration file: /Users/yourname/yourname.github.io/_config.yml
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
{% endhighlight %}
此时我们打开浏览器，在地址栏输入：
<code>localhost:4000</code>或者<code>127.0.0.1:4000</code>就能看到我们的博客了。


> 接下来创建一个<code>_layout</code>文件夹，在这里创建3个文件：

####默认模板<code>default.html</code>

(是所有页面的父类。)

{% highlight HTML %}
<!DOCTYPE html>
<!--请删除代码中的"\"-->
<html>
	\{\% include head.html \%\} # 在_include文件夹下搜索head.html并加载。
<body>

	<div class="container">
		\{\% include header.html \%\}
		\{\% if site.default_column == "two" \%\}  # 如果站点样式是“双列”，如下显示：
			<div class="page-content col-sm-8">
				\{\{ content \}\} # 加载_posts/xxxx.MD文件中的内容。
				\{\% include post_pagination.html \%\} # 在_include文件夹里搜索post_pagination.html并加载。
			</div>
		\{\% include sidebar.html \%\}

		\{\% else \%\} # 如果站点样式是“单列”，如下显示：

			<div class="page-content">
    			<div class="wrapper">
      				\{\{ content \}\} # 加载_posts/xxxx.MD文件中的内容。
    			</div>
  			</div>
  		\{\% include post_pagination.html \%\} # 在_include文件夹里搜索post_pagination.html并加载。
  		\{\% endif \%\}
		\{\% include footer.html \%\} # 在_include文件夹里搜索footer.html并加载。
	</div>
</body>
</html>

{% endhighlight %}

####页面模板<code>page.html</code>

{% highlight HTML %}
<!--请删除代码中的"\"-->
---
layout: default
---
<div class="post">

  <header class="post-header">
    <h1 class="post-title">\{\{ page.title \}\}</h1>
  </header>

  <article class="post-content about"> 
    \{\{ content \}\}
  </article>

  \{\% if page.comments \%\}
  \{\% include comments.html \%\}
  \{\% endif \%\}

</div> 
{% endhighlight %}

####博文内容模板<code>post.html</code>

{% highlight HTML %}
<!--请删除代码中的"\"-->
---
layout: default
---
<div class="post">

  <header class="post-header">
    <h1 class="post-title">{{ page.title }}</h1>
    <p class="post-meta">
    \{\{ site.locales[site.default_locale].PostedInCategories \}\}
    \{\% for cat in page.categories \%\}
    <a href="{{site.baseurl}}/categories/#{{ cat }}">{{ cat }}</a>&nbsp;
    \{\% endfor \%\} 
    \{\% if page.tags != empty \%\}
    \{\{ site.locales[site.default_locale].Taggedwith \}\}
    \{\% for tag in page.tags \%\}
    <a href="{{ site.baseurl }}/tags/#{{ tag }}" title="{{ tag }}">{{ tag }} </a>\{\% unless page.tags.last == tag \%\}, \{\% endunless \%\}
    \{\% endfor \%\}
    \{\% endif \%\}
    \{\{ site.locales[site.default_locale].PostDate \}\}\{\{ page.date | date: "%b %-d, %Y" \}\}
    </p>
  </header>

  <article class="post-content">
   	\{\{ content \}\}
  </article>
  <hr />
</div>


\{\% include page_pagination.html \%\}
\{\% include comments.html \%\}
{% endhighlight %}

你看，为了写这三个模板，我们又要给模板里丰富板块，所以又要增加更多的页面……<br>
于是我们把网站的目录结构变成如下样子：
{% highlight Bash shell scripts %}
# 这里的内容请参考上面的逻辑来自己写！
.
├── _backup
│   ├── en.tar.gz
│   └── style.css
├── categories                              # eg: => http://yulijia.net/en/categories/ 
│   └── index.md
├── _config.yml
├── css
│   └── main.scss
├── feed                                    # eg: => http://yulijia.net/en/feed/index.xml
│   └── index.xml
├── guestbook                               # eg: => http://yulijia.net/en/guestbook/
│   └── index.md
├── home.md
├── _includes
│   ├── Aboutme.html
│   ├── Archives.html
│   ├── Blogroll.html
│   ├── Categories.html
│   ├── comments.html
│   ├── Copyright_Notice.html
│   ├── footer.html
│   ├── header.html
│   ├── head.html
│   ├── page_pagination.html
│   ├── post_pagination.html
│   ├── Recent_Posts.html
│   ├── sidebar.html
│   └── Tags.html
├── index.html
├── _layouts
│   ├── default.html
│   ├── page.html
│   └── post.html
├── _posts
│   ├── 2011-07-22-hello-world.md
│   ├── 2011-08-06-how-to-calculate-word-frequencies-with-r.md
│   ├── 2011-08-18-should-draco-be-effective-against-virtually-all-viruses.md
│   ├── 2011-10-21-why-viruses-produce-long-dsrna-but-not-endogenous-ones.md
│   ├── 2012-03-22-100-things-bioinformatics-students-should-do-before-graduating.md
│   ├── 2012-10-08-a-new-site.md
│   ├── 2012-10-09-github-pages.md
│   ├── 2012-10-22-a-conference-of-Genomics-and-Epigenomics.md
│   ├── 2012-10-23-CSHL-Asia-interesting-talks-on-genomics-and-epigenomics.md
│   └── 2013-01-30-how-to-get-RefSeq-gene-annotations-from-UCSCdatabase.md
├── README.md
├── _sass
│   ├── _base.scss
│   ├── _layout.scss
│   └── _syntax-highlighting.scss
└── tags
    └── index.md
{% endhighlight %}

之后就可以发布博文了：<br>
首先文件名一定要符合如下规范：

> # YYYY-MM-DD-post-name.md
> 2015-03-20-how-to-use-jekyll.md<br>
> #不要使用中文，有时候会出错。保存格式为markdown。jekyll编译器就会自动替换掉模板内的\{\{ content \}\}。

然后保存在<code>_posts</code>文件夹下

{% highlight Bash shell scripts %}
# 这三个横线之间就是帖子的设置，这些不会显示在博文里。
---
published: true # 是否已发布
title: Hello world! # 帖子名称，用来显示在index.html中。如不写，Jekyll则用文件名来代替。
layout: post # 应用哪一个模板，博文模板就用post。
author: yourname # 作者名，如不写则默认为网站拥有者的名字。（_config.yml里author设置的名字。）
category: Uncategorized # 仓库类别
tags: HelloWorld # TAG标签
---
# 下面就是帖子将要显示的内容
Hello world! This site is my first English blog. 
{% endhighlight %}

> ## 刷新一下浏览器看看效果吧！

附录：[《使用Jekyll搭建一个博客 (三) － 排版格式》](/tutorial/2015/03/20/blog-format.html)


