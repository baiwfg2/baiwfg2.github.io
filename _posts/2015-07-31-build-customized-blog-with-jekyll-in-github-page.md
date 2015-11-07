---
layout: blank
title: 用Jekyll在GitHub Pages中创建定制化的博客
category: tech
tags: jekyll 
comments: true
---

## 基本工具准备
博主的试验环境是在centos 7.0上的，像这种开源的东西肯定是得放在linux环境下用的，如果读者的环境是windows，保不准出问题，虽说官方也支持。在正式开始之前，建议读者先大致看看文章最后给出的几个参考链接，真心有价值，博主也是从他们那里获取了基础知识。正所谓站在别人肩膀上前进，确实如此。大致看了之后，让我们开始吧。

### Ruby安装
在centos下安装ruby是很容易的，它会附带gem命令。直接用如下命令：
> yum install ruby 

### Ruby源更改
因为使用默认源是无法安装jekyll的。做法如下图所示，具体内容可见参考链接第3条

![install-rubygem-from-mirror](/assets/post-images/install-rubygem-from-mirror.png)
### 安装jekyll 
直接使用如下命令搞定：
> gem install jekyll 

打印安装信息，如果正常的话就安装成功了
### 小试牛刀
如果急于想测试下jekyll的有效性，可以按如下基本步骤来做：

1. jekyll new myblog

	myblog是根目录名称，接下来生成的文件都在其中。如果此命令执行时出现javascript相关错误，应该是需要安装nodejs

2. cd myblog 
3. jekyll serve

此时在myblog目录下就生成了基本目录和文件。关于各目录的介绍，参考链接中的博文已经讲了很多了，
我就不在这嚼舌根了。强调一点：\_site目录是在第三步之后才有的，内部其实进行了build操作。
可基本理解为jekyll为除\_site目录外的所有内容生成了静态网页并保存在\_site下，这样如果发布
网站只需上传\_site下的内容即可。

运行效果如下：

![jekyll-serve](/assets/post-images/jekyll-serve.png)

注意下面的regenerating是表明我修改文章后能很快检测出来重新生成，这样方便了很多

启动本地web程序，在localhost:4000可访问

## 建立自己的blog
光有jekyll不行，还只是在本地跑，得放在互联网上。幸亏有github做了件有趣的事，允许用户在
github page上托管网页，后台支持jekyll。几个git操作就可将静态网页放到某个分支上，就可用
独立域名访问了，还免流量，不像wordpress那样麻烦（当然人家也高端，支持动态生成）。
所以若想建立中小型的简单博客，jekyll+github还真挺好。

正如链接一中网友所说，有三种方式：从头开始、找一份框架修改使用、fork别人的。身为<font color="red">前端学渣</font>，也只好用fork了。
我直接fork了[这里](https://github.com/minixalpha/StrayBirds/tree/gh-pages)。
因为发现这里提供挺好看的框架，而且作者也打包了，直接修改配置文件就能用，较合心意，接下来的讲述也是以此仓库为标准。
基本打算就是先下下来，在本地跑起来，弄清楚基本的概念，添加一些文章看看变化，熟悉之后再托管到自己的github上去。

### 修改配置文件
git clone之后，首先关注的是_config.yml文件。里面的参数都得定成自己的。最为关键的值如下：

* username

要改成自己的github用户名，因为到时要用***用户名.github.io***来访问，具体教程可参考[这里](https://pages.github.com/);

* baseurl

我给改成了空，这样就是直接用master分支作用户博客的来源了，而不是项目站点中用的gh-pages分支。关于这一点，若有不懂请读者认真阅读链接一博文。

* excerpt_seperator

当显示文章摘要时，这个选项就很好用的。只要人为地在文章中加入相应字符就可显示出摘要而不是全部，美化了页面布局。默认是\n\n\n

### 关于主题
默认使用的是kunka主题，位于themes目录下。博主还是非常喜欢kunka主题的，就是背景颜色稍需调整，而且有导航，挺像一个正式上线的网站。midnight主题也挺不错，可惜没导航，kunka里面的很多都没有。
不过也没关系，先学会kunka主题，肯定是有地方进行更改的。

### 编写自己的文章
文章支持markdown,html等格式，在_post目录中。由于博主已经比较熟悉markdown语法，所以就删除了不相关的文件，建立了自己的两个文件，一个是html格式，是曾经生成的一个文档；另一个是md格式，正是此篇文章，用markdown语法编写。

注意每篇文章前面都有个头部，用以标识本篇文章的一些属性，它最后会被jekyll生成对应的html格式文档。例如本篇post的头部是这样的：

> \-\-\-

> layout: post

> title: 用Jekyll在GitHub Pages中创建定制化的博客

> category: tech

> tags: jekyll 

> \-\-\-

layout:采用了_layout目录中的post.html 

title:文章标题

category:文章分类，便于管理，也可以用复数categories表示层级分类目录

tags:文章标签

还有一个不常用的域permalink，可以自定义文章的url。默认是以年月日加题目的，如果感觉不爽可更换。更多详细设置在[这里](http://jekyll.bootcss.com/docs/configuration/).且写的时候一定要注意：<font color="red"><strong>冒号后面至少要加一个空格，没有空格会报错</strong></font>

### 关于代码高亮
既然在github搭了博客，肯定是要上代码，那这时候代码好不好看就是个问题。
之前在[这篇文章](https://baiwfg2.github.io/tech/2015/07/31/build-customized-blog-with-jekyll-in-github-page.html)中介绍过基本搭建，也从[这里](https://github.com/minixalpha/StrayBirds/tree/gh-pages)下载了源码进行研究，但发现作者本来的代码高亮是令人遗憾的，丑得吓到我了，如下图：

![normal-effect](/assets/post-images/normal-effect.jpg)

于是想办法搜索在jekyll中实现代码友好高亮的方法，现查到有两种方式，接下来分别讲述。

#### 借助syntaxhighlighter实现代码高亮
目前找到的参考教程有两个：[这里](http://www.cnblogs.com/heyuquan/archive/2012/09/28/2707632.html)和[这里](http://ju.outofmemory.cn/entry/79518)

按照教程指示，我找到了_includes/kunka.html文件(默认主题是kunka)，把里面引入themes/css/syntax.css的link标签给注释掉，添加了以下内容：
![](/assets/post-images/added-link-css.jpg)

生成的c,python(其它语言类似)默认主题代码样式是这样的(注意此时不要用markdown的```或者Liquid语法了，用pre或script标签)：

由于官网[http://alexgorbatchev.com](http://alexgorbatchev.com)是国外的，访问可能会有些慢，但目前还能接受。当然你可
选择将相应的文件下到本地引用，这样就快了。
当然还有其他风格的，像eclipse,emacs等，读者可以自行尝试。

#### 使用pygments实现代码高亮
参考教程在[这里](http://havee.me/internet/2013-08/support-pygments-in-jekyll.html)

此法待续...

### 运行测试
刚开始运行时，响应缓慢，浏览器下端显示了font.google的字样，估计是加载谷歌字体的问题。
通过搜索发现可用[font.useso.com](http://libs.useso.com)和[ajax.useso.com](http://libs.useso.com)
来分别替换google网站的font和ajax。替换后就正常了。至于哪些文件有这个链接，用find+grep+bash很容易找到。

首页效果如下图所示：

![jekyll-blog-show](/assets/post-images/jekyll-blog-show.png)

上一篇就是本篇文章，下一篇是html格式文章；右边有部分字体比较奇葩，我想就是useso.com提供的

## 参考链接
* [使用GitHub,Jekyll 打造自己的免费独立博客](http://blog.csdn.net/on_1y/article/details/19259435)
	* 这是博主学习jekyll的启蒙文章，非常感谢作者提供了StrayBirds和他自己博客的源代码信息
* [jekyll中文教程](http://jekyll.bootcss.com/docs/home/)
	* 貌似是国内有人翻译的，很好，就是有点慢
* [RubyGems下载](http://ruby.taobao.org/)
	* 国外的ruby貌似被挡了，所以国内有人做了镜像，真是大好银啊
* [github jekyll](https://github.com/jekyll/jekyll)
* [搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)
	* 这是篇很经典的日志，值得参考，但要注意有些地方已经有改动了
* [使用jekyll来写博客的一些心得](http://www.tuicool.com/articles/vENfq2)
	* 谈到了更多操作，像评论系统可用国内的多说、友言，代码高亮等
* [github markdown语法介绍](https://github.com/baiwfg2/README)
