---
layout: post
title: "就来谈谈产品开发"
author: xenonchau
summary: |
 <h4>"现学现卖，谈谈关于产品开发中的一些问题。"</h4>
 <p>iOS开发中，code、xib和storyboard哪一个更好？</p>
 <p>如何开发一款让用户感觉舒服的软件？</p>
 <p>从零开始开发一个产品都有那些要注意的？</p>
category: 技术文章
tags:
- Production
---


###iOS开发中，code、xib和storyboard哪一个更好？

我们先看一下历史：

xib(Interface Builder)在早期的iOS SDK中就已经出现了。<br>
Apple从Xcode 4开始就开始就将xib直接集成在IDE中了。<br>
其后在4.2版本里又新增了storyboard，使xib的逻辑关系更加好梳理。<br>
Apple在Xcode 5.0的时候开始不遗余力的推广storyboard，连Stanford的[Paul Hegarty](http://en.wikipedia.org/wiki/Paul_Hegarty "see Wikipedia")也在[Stanford Open Course - CS193P -Fall2013](http://web.stanford.edu/class/cs193p/cgi-bin/drupal/downloads-2013-fall)中基于storyboard教学了。（[最新的course是iOS 8和Swift开发](https://itunes.apple.com/us/course/developing-ios-8-apps-swift/id961180099 "view in Itunes U")）<br>
再到现在的AppleWatch更是强制开发者必须用storyboard来开发。<br>
可见storyboard已经是不可逆的大趋势了。

> 那我们要如何选择适合自己的方法呢？

我们再来分析一下三者之间的优劣：

* ####code

	用纯代码来书写一个app，首先这看起来就是一个“高大上”的方式。<br>
	代码“基本”无所不能，而且可重用度高，兼容性好，是历史最悠久的编程方式，而且对于深入理解每个控件的实现原理很有帮助。<br>
	但即使纯代码编程这么强大那也一定会有弱点——对，就是“慢”！<br>
	而且对于现在碎片化的屏幕尺寸来说，适配屏幕也是纯代码编程的弱项，需要用大量的代码来进行判断。但在IB中，只需要利用 <code>Autolayout</code> 进行适配即可。

* ####xib

	上面提到过，在Xcode初期就已经出现了xib的身影，而且据说绝大部分Apple自家的app都是用IB开发的。<br>
	xib最大的特点就是所见即所得(WYSIWYG)，优势就是比code创建控件更快。而且对于MVC架构的理解更加直观，对初学者来说甚好！<br>
	但是其缺点也很明显——每个xib都是单独的页面，不能用一种全局的视角对项目进行分析，让业务逻辑显得非常混乱。

* ####storyboard

	storyboard可以看做是一组xib的集合，这样就有效的避免了业务逻辑混乱的局面。<br>
	在storyboard中可以很清楚直观的看到页面间的跳转，无论是做产品原型还是敏捷开发都非常适合。<br>
	它的最大的缺陷就是缺乏可重用性，每个控件都是单独的存在，在效能方面来说有些欠佳。不过对于iPhone5以上的机型来说，这些性能差距已经可以忽略不计了。<br>
	有些同学比较担心协同开发的时候如何用storyboard？这大可不必担心——没人规定一个app中只有一个storyboard，每一个功能模块单独一个storyboard也不是不可以的。

> 总结一下：

&nbsp;&nbsp;&nbsp;&nbsp;我建议用storyboard来进行产品原型设计以及框架搭建。
对于一些可重用性高的页面或者控件，用纯代码来实现——例如“抽象工厂”。
用xib来解决storyboard不允许单个view存在的问题——例如“自定义 <code>UITableViewCell</code>。

<hr>

###如何开发一款让用户感觉舒服的软件？

> 简单来说就是用户体验。

* 用户体验（User Experience，简称UE/UX）是一种纯主观在用户使用产品过程中建立起来的感受。*

> 如何从用户角度设计app

1. 关注用户的操作习惯
	* 用户都非常懒——操作步骤能少就少。
	* 据统计：在用户体验到内容之前就要求注册，卸载率会高达90%。除非是IM类的app。
2. 充分考虑app的使用环境
	* 对应不同使用环境来设计app的功能。
3. 尽量减少app的访问级别
	* 简单的说就是不要嵌套太多逻辑关系。
	* 不要在app内加入太多可有可无的功能。PM要懂得缩减界面、删功能。
4. app功能设计要分清主次
	* 甲方看见产品原型之后会迸发出无限的想像力。
	* 页面设计要渗透80/20定律([Vilfredo Pareto定律](http://en.wikipedia.org/wiki/Vilfredo_Pareto "see Wikipedia"))。
5. 尊重用户的劳动成功
	* 用户无需二次重复操作。eg: 自动保存离线内容。使用户感觉到方便。
6. 尽可能的减少用户输入
	* 如果必要，应给出相关提示。eg: 操作完成、输入之后会验证合法化。

<hr>

###从零开始开发一个产品都有那些要注意的？

> 在把一个想法付诸行动之前，我们有以下工作要做。

1. 产品需求文档(Production Required Documents - PRD)
	* 需要注意的是不要“坐井观天”将自己的喜好普遍化，市场调研一定要真实可信。
2. 分析竞争对手
	* 一个产品也许以及有很多对手在做，我们可以分析它的产品的薄弱环节，专精这一点来争取到市场份额。

<hr>

> <center>全文完</center>

写得很浅薄，欢迎大家留言指点。
