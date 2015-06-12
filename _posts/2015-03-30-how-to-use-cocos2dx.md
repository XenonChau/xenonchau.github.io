---
layout: post
title: 用cocos写一个游戏
author: xenonchau
summary: |
 <p>
 首先假设各位看官都熟悉C++，而且都知道cocos2d-x。
 </p>
 <p>
 接下来，让我们一步一步的写一个简单的小游戏吧。
 </p>
---

###准备工作

首先我们要确定要做什么样的一个游戏——一个靠手指拖拽精灵(Sprite)进行搭建各国建筑物的幼儿游戏(因为很简单，所以定位是幼儿游戏)。

在确定了游戏方向之后，我们要策划一下游戏的具体样子以及操作逻辑，并用Aurex等原型软件做一个产品原型——这里就不累赘了，我们主要来讨论代码逻辑。

之后让美工把图片按照要求切割成合适的大小。之后就可以进行场景搭建了。

###搭建场景

用代码来控制一个游戏的布局十分蛋疼，还好触控科技给我们提供了一整套完整的开发环境。这个时候我们就要用到cocos的一个软件——CocoStudio。

创建工程的时候请一定要注意工程名和包名一会都会按照这个软件里写的发送到Xcode里，不要想着先随便写以后再改。

在CocoStudio中按照产品原型把图片铺好，并把每一个图片都用英文准确的命名——这一步很重要，之后在代码中操作每一个控件都需要这个名字。
每一个控件具体是Image、还是Sprite、或者是Button，最好在脑袋里想清楚，不然以后再想改动很费时的。

这里要注意的是：MainScene.csb是必须存在的，你的第一个视图导入其他名称的会出现问题——我也不知道为什么，反正我这边报错了。

在确定了所有的控件都按照原型图拜访好之后，点击<code>File</code>-><code>Publish</code>-><code>Publish to Xcode</code>。

###导入场景进行控制

新建C++ file，然后把scene必要的方法写出来。

在这里我们为了简化教程，把之后的逻辑都在init()方法里实现了。

{% highlight cpp %}
//为了使用CocoStudio导入的场景文件，我们需要引用几个库。
#include "cocos/CocoStudio.h"
#include "ui/CocosGUI.h"

//这样就获得了全部的场景文件
auto rootNode = CSLoader::createNode("MainScene.csb");

//然后把这个文件(Layer)添加到this上。屏幕上就能显示出来我们创建好的场景了。
this->addChild("rootNode");

//获取rootNode上的控件
auto widget01 = static_cast<Sprite *>(rootNode->getChildByName("ConfigButton"));//这个""内的字符串就是我们在CocoStudio中每个控件的名字。

//让我们获得的控件动起来
widget->runAction(MoveBy::create(0.5f, Vec2(100, 0)));//第一个参数是时间，第二个参数是移动后的位置。

//看！就这么简单！


{% endhighlight %}



