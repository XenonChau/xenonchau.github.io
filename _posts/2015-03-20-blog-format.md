---
layout: post
title: 使用Jekyll搭建一个博客 (三)
summary: 排版格式
category: tutorial
tags:
- WebSite
---

##附录：排版格式

<hr>

# &#35;一级标题

## &#35;&#35;二级标题

### &#35;&#35;&#35;三级标题

#### &#35;&#35;&#35;&#35;四级标题

*&#42;斜体&#42;*<br>
**&#42;&#42;粗体&#42;&#42;**<br>
***&#42;&#42;&#42;粗斜体&#42;&#42;&#42;***

&lt;cite&gt;这是一条引用文字&lt;/cite&gt;<br>
<cite>这是一条引用文字</cite>. 

&lt;u&gt;下划线&lt;/u&gt;<br>
<u>下划线</u>. 

&lt;del&gt;删除线&lt;/del&gt;<br>
<del>删除线</del>. 

Water is H&lt;sub&gt;2&lt;/sub&gt;O. 
Water is H<sub>2</sub>O. 

<hr>
&lt;code&gt; 这里写代码 &lt;&#47;code&gt;<br>
<code>这里写代码</code>

&#123;&#37; highlight ruby &#37;&#125;<br>
这里写大段的代码<br>
&#123;&#37; endhighlight &#37;&#125;<br>
{% highlight ruby %}
这里写大段的代码
{% endhighlight %}
这个highlight支持很多种语言，可以查阅以下链接：

1. [Pygments Supported languages](http://pygments.org/languages/)
2. [Pygments online deme](http://stackoverflow.com/questions/9652490/do-i-need-to-generate-a-css-file-from-pygments-for-my-jekyll-blog-to-enable-col)

<hr>
&#91;这里是超文本链接的文字&#93;&#40;这里是链接的内容&#41;<br>
[这里是超文本链接的文字](http://#)

&#33;&#91;图片介绍&#93;&#40;https://avatars2.githubusercontent.com/u/11521664?v=3&s=460 &quot;鼠标悬停文字&quot;&#41;<br>
![图片介绍](https://avatars2.githubusercontent.com/u/11521664?v=3&s=460 "鼠标悬停文字")

<hr>
## 块引用

> Justification:
> This species is listed as Extinct in the Wild, as all populations are still under captive management. The captive population in China has increased in recent years, and the possibility remains that free-ranging populations can be established some time in the near future. When that happens, its Red List status will need to be reassessed. 


> I follow up the quest. Despite of day and night and death and hell.
> <center> -- Idylls of the King, Tennyson </center>

<hr>
### 有序列表
{% highlight Bash shell scripts %}
1. 大标题 一
   1. 小标题 1
   2. 小标题 2
   3. 小标题 3
2. 大标题 二
{% endhighlight %}
1. 大标题 一
   1. 小标题 1
   2. 小标题 2
   3. 小标题 3
2. 大标题 二

### 无序列表
{% highlight Bash shell scripts %}
* 列表 1
* 列表 2
* 列表 3
{% endhighlight %}
* 列表 1
* 列表 2
* 列表 3

<hr>
### 表格
{% highlight Bash shell scripts %}
| Header1 | Header2 | Header3 |
|:--------|:-------:|--------:|
| 左对齐   | 居中对齐 |   右对齐 |
| 左对齐   | 居中对齐 |   右对齐 |
| 左对齐   | 居中对齐 |   右对齐 |
{% endhighlight %}

| Header1 | Header2 | Header3 |
|:--------|:-------:|--------:|
| 左对齐   | 居中对齐   | 右对齐   |
| 左对齐   | 居中对齐   | 右对齐   |
| 左对齐   | 居中对齐   | 右对齐   |


