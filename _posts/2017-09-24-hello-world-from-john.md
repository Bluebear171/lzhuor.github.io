---
layout: post
title:  "Hello World, John! 以后聊聊技术，严肃活泼地。"
image: ''
date:   2017-09-24 00:00:00
tags:
- mongodb
description: ''
categories:
- Learn Jekyll 
---

<p class="music-read"><iframe src="https://open.spotify.com/embed/track/4w2Yq2cklbssmUtUy5Vh6H" width="300" height="80" frameborder="0" allowtransparency="true"></iframe></p>

## 从哪里说起呢?
{% highlight javascript %}
const sayHelloWorld = () => console.log('Hello World!');
sayHelloWorld();
{% endhighlight %}

然然自己觉得很多事情像刚学习一门编程语言时写Hello World一样 - 看到屏幕上出现"Hello World!"的一秒钟感觉这件事情很简单嘛，仿佛自己打开了新世界一般激动。然而用不了多久这个激情就会消退，剩下的是无尽的拖延。

举个不恰当的例子，很早就想搞一个这样的博客，不用太复杂，只要有个地方分(chui)享(niu)自己做开发时候解决的有意思的问题。然而一拖再拖，一是因为不知道这种博客怎么搭建 
(十万个为什么一般: 是静态还是动态？是用HTML模板还是Markdown? 读者评论怎么搞? 此处省略一万字...)。 结果有一天跟万总([@sfdye](https://github.com/sfdye)）
学习的时候知道了原来有个叫 [Github Pages](https://pages.github.com/) 的东西。等等，万总是单身，女同学们不是老说给介绍优质单神男性，快砸向万总啊。
GitHub Pages写博专用而且免费提供host（之前自己的server放在AWS EC2，有点牛刀割鸡的感觉) 
于是今天然然子就花了些时间搭建起来了这个东西，学名 [Jenkyll](https://jekyllrb.com/)，真的棒👍，简单实用。
然然子虽然很然很贪玩，但是码起来毫无含糊。你看这眉头，还有多多说我的肥手就像叮当猫。

<img src="/assets/img/posts/2017-09-24-hello-world-from-john/hello_world_john.jpg">
顺便说一下，NUS Utown真**的适合学习，为啥当初在SMU就没个这种安静空旷满眼绿色的地方。

## 言归正传

为什么想搞一个这个自己的Web呢？并不是自我感觉良好觉得自己都可以教人了。参加了一些MeetUp，越来越觉得自己是初学者。最怕"You think you know but you don't know."和"You don't know what you don't know." 所以总结一下初衷，主要一下三个原因吧。

### 1. 然然一直觉得把一个东西做出来和把一个东西讲出来是完全两码事。
讲一个东西需要把知识的任督二脉打通，这样跟别人讲起来才能不讲成然然子。我经常给多多（不是🐶，是我老婆）讲一些很基本的东西的时候发现很费劲，一开始总觉得她是外行，后来读了别人的文章才发现复杂的东西也可以讲得简单易懂，基础的东西也可以讲得水落石出。

### 2. 希望可以分享技术，长江后浪推前浪，自己不更新自己很容易失去竞争力。
矫情点装逼点讲做开发是个青春饭，趁年轻不多积累点等以后和主流技术脱轨，竞争力必然下降。
有了竞争力能不能改变世界不说，至少可以让生活质量再好一点吧，谁不希望靠勤劳的双手改善一下生活呢？什么?！你说你15年初投了点比特币? 再见朋友...

### 3. 来我们一起唱 "我想要有个家，一个不需要多大的地方"。
对，在WWW的世界里，我也要想有一个片自己的家，可以说话的地方，记录生活与技术的点点滴滴。

当然，然然可能不定期插播做饭和家常家短...

## 简单总结一下开工的这一年
当然要提一下在纽约的一个半月。我以为走上了人生巅峰（说白了还是活在别人眼里，虚荣心在捣鬼）。住在WTC旁边的套房，每天training水到不能再水，翘课、喝酒、美食、见朋友就成了日常，也认识了和我一起刀塔一起GG一起离职的Yisheng同学。
然而残酷的现实是在银行做技术就像你非要在中国闹革命一个道理，想用点新技术学点开源库? 阻力大的你都别管了。
于是在一个先我离职的Developer的洗脑下加入了现在的这个Start-up。

一开始我是坚决抵触加入创业公司的，因为早期还是想要有一个enterprise水准的开发环境。我印象中小公司的Software Development Life Cycle (SDLC)、代码规范、做事风格总让人觉得颤颤巍巍。总担心自己得不到足够的指导因而不能得到提升。
但是当时在银行里做开发实在不开心，觉得像个行尸走肉，技术上难有大突破，经常性重复自己。然后问了一下新工作用不用JIRA，有没有DevOps这个环节。他们说用JIRA，有Confluence(wiki)，有Jenkins，不是Trunk base但是是Git workflow。
然后这边前端是现在流行的React+Redux，后端有Node.js，有MongoD, 有object mapping (mongoose)，还有Scala，Cassandra，Akka这些比较时髦的东西。于是就拍拍脑袋辞职了。记得前一个周五才和可爱的老板去打了板球，接着周一就辞职了，
有点尴尬。

总的感受，高盛作为银行业大哥之一，人文和工作环境真的不错，同事们都很professional，很有耐心，做事也负责。自15年暑假实习、16年7月到17年6月的这段回忆总的来说我是非常感激的。
见识到了Enterprise水准的Java，也在写SecDb/Slang中领会了更多的Functional Programming、面向对象(OOP)的精髓。感激！做了这个网站纪念一下 http://www.girtech.sg

现在的公司年轻人居多，做事节奏快效率高，沟通上也没什么问题，不用凡事Polycom，更没有时差。而且Yisheng和我一起过来了，可以做个伴😆。唯独我自己感觉欠缺一点银行里的规范性。虽然我们现在test coverage高的惊人，但是Quality Assurance和技术文档上还欠缺很多功夫。慢慢来吧，不可能一口吃个胖子。
很欣慰的是整个SDLC和DevOps的流程有板有眼的在进步。希望会越来越好，我是非常有信心的。

不管怎么样，我相信没有一个工作的地方是完美的，还是要修炼自己。三十岁之前还是想去Google, Facebook, Amazon这种水平的公司去做做开发。差的还很多，继续努力。说到这里想到了LeetCode，拖了一年了还没开始真正的刷。典型废柴然然子一个！自制力特别cà...

## 说说接下来更新的计划吧
扯了很多没有营养的，准备先发两篇技术文章吧。

之前一直在用Babel来解决JavaScript语法糖在不同版本的引擎之间兼容性的问题，但是并不了解原理（吃了不是Computer Science科班出身的亏，后来知道NUS School of Computing有专门学compiler的课。最近因为遇到了几个刁钻的bug，不得不folk了别人的babel-plugin，打开了JavaScript transpiler的大门。所以接下来第一篇文章简单地聊一下ESTree，JS源代码到AST以及Babel插件的原理吧。

然后准备聊一下跨域名的Cookie植入如何实现，业界经典案例要属Google Analytics的第三方Cookie植入了吧。然后还准备聊一下一个实战应用：如何实现多面板同时登入登出。感兴趣的话可以去试着开两个Gmail的登录窗口，随便登录一个另外一个会自动登录跳转。

接着想说一下Behavior-Driven-Development(BDD)的实际应用。目前能想到的都这些吧，恕然然水平有限，之后有想到的话题慢慢更嘛。争取能中英同步，不过咱们中文博大精深，有的这个名词真的是牛逼。比如deployment叫部署。Production叫生产环境。我继续学习。

另外去年底求了婚，前一阵拍了婚纱照lol... 感叹Time flies. 珍惜时间，早日圆Google梦。充充实实地过，疯疯癫癫地乐。
<img src="/assets/img/posts/2017-09-24-hello-world-from-john/duoduo_ranran_pre_wedding.png">
