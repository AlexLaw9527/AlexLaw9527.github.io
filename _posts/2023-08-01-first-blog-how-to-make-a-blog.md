---
date: 2023-08-01 2:02:22
layout: post
title: 利用GitHubPages搭建一个博客
subtitle: 真正的第一篇文章
description:
image: https://www.baidu.com/img/PCtm_d9c8750bed0b3c7d089fa7d55720d6cf.png
optimized_image:
category: blog
tags:
author: alex
paginate: false
---
<!-- # 利用GitHubPages搭建一个博客 -->
利用GitHubPages搭建一个博客很简单，难度评级为像我这种零基础的也两个半小时就上手
分两步走
首先先在先在你本地搭建Jekyll的环境，再在GitHubPages上套用你想要的模板就好了，十分简单。


这里我参考的是Spencer Pao的教学视频，Spencer Pao在[How To Build A Website | Github Pages | Jekyll | Template](https://www.youtube.com/watch?v=g6AJ9qPPoyc)中演示了如何套用一个模板，如何修改他的关键信息。
**al-folio**也很不错，他的主页上看到fork人数超多已经足以证明它的泛用性和受大众的喜爱程度。
这里笔者使用的是名为[**jekflix-template**的Jekyll模板](https://github.com/thiagorossener/jekflix-template)，他的页面上也给出了[这个主题的demo页面](https://jekflix.rossener.com/)


## 本地搭建Jekyll的环境
搭建环境部分中，[从零开始设置 Jekyll | zhihu](https://zhuanlan.zhihu.com/p/37931567)一文中讲的非常详细。
搭建好基本框架之后就可以结合**jekflix-template**的指引一步一步走，这里笔者推荐下载一个GithubDesktop，这样可以省下一些时间，毕竟git的学习成本也挺高的[^git学习成本]。
[^git学习成本]: 笔者之前一直搁置搭建这个GithubPages就是因为git一直没有办法提交（clone是成功的，大概率是笔者登录的问题），之后也许还会再去尝试。为了节省时间和少走弯路还是推荐使用GithubDesktop


直接看**jekflix-template**的指引的**Setup**部分
>In the case you're cloning this repo, follow those instructions:
>* Environment
>* Installing template
>* Running local


然后点进[**Environment**](https://github.com/thiagorossener/jekflix-template/blob/master/docs/setup.md#environment)就可以进行环境的配置。
>Before starting, make sure you have Ruby and NodeJS installed.

关于Ruby的安装，[从零开始设置 Jekyll | zhihu](https://zhuanlan.zhihu.com/p/37931567)一文中讲的非常详细。不需要全部看完，看到
>直到看到 ** gems installed ，输入 jekyll --version ，有版本号就表明安装完毕。

就可以了。
然后NodeJS的安装直接进到他们的[下载页面](https://nodejs.org/en)，下载LTS版本或者最新版都可以，然后安装，下一步下一步，最后的安装工具得到选项不需要勾上，不然会帮你安装很多东西（python3、vss的生成工具等）。

然后继续按照步骤
安装Jekyll:
```
$ gem install jekyll
```
安装Gulp client:
```
$ npm install gulp-cli -g
```

## 安装模板
1. 首先Fork这个[**Jekflix Template**](https://github.com/thiagorossener/jekflix-template/fork)这个项目，名字一定要按照**GitHubPages**的命名要求
2. 然后Clone这个项目（你自己的repo，存储库的源码）到你本地（推荐使用**GitHubDesktop**进行克隆，但是不要选到给这个项目做贡献，而是选择二次开发）
```
#使用GitHubDesktop进行克隆的话不需要输下面这行命令
$ git clone https://github.com/<your-github-username>/jekflix-template.git
```
1. 切入你Clone的文件夹（假装科普一个更快的方法，使用**GitHubDesktop**进行Clone之后，对着你Clone的项目右键可以在文件管理器中打开，然后直接在文件管理器的地址栏里面，（先清空，再）输入cmd，然后回车，这个时候你就是在这个文件夹的cmd，就不用cd进去）
```
$ cd 你Clone的项目的位置
```
1. Install npm packages:
```
$ npm install
```
1. Install Ruby dependencies:
```
$ bundle install
```
***
注意，在这里你有可能会遇到一个很奇怪的bug，就是你输入像使用`bundle install`后无响应问题的问题[^bundle_install长时间无响应] ，可以尝试先输入
```
$ bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```
然后再执行
```
$ bundle install
```
[^bundle_install长时间无响应]: 参照[bundle install 无响应问题](https://cj1406942109.github.io/2018/11/17/bundle-install-no-response/)和[bundle install 长时间无响应解决办法 | CSDN](https://blog.csdn.net/qq_24395387/article/details/103893335)进行解决

***
1. Build Jekyll:
```
$ bundle exec jekyll build
```
1. Then run Gulp:
```
$ gulp
```
在输入`gulp`之后这个静态网站就已经跑起来（或者应该叫渲染出来了），你可以在cmd里面看到你本机可以访问这个网页的地址和一个（内网）外部访问的地址（带有端口号）

## Running local

After the steps above, to run Jekyll locally, you'll just need to run Gulp:
```
$ gulp
```
如果看到前文提到的网址，表示本地的博客服务已经建好，在窗口按下` ctrl `键加` C `的组合键，就可以结束服务。在关闭命令提示符窗口之前必须先手动结束服务。

>GitHub pages
>It's a known issue that you can't run Gulp when deploying the website into GitHub pages. So, you must change the theme colors and run ` gulp build `locally, then push the changes into your repo, there is no other way.
>To see how your website is going to look like when you deploy it, run bundle exec jekyll serve and access `http://127.0.0.1:4000/`.


关于提示：Auto-regeneration: disabled. Use --watch to enable

这条消息表示自动重建功能已被禁用。自动重建是Jekyll的一个功能，它会监视您的源文件夹中的更改，并在更改后重新构建您的站点。这意味着，如果您对源文件进行了更改，您的站点将会自动更新。

要启用自动重建，您需要在运行jekyll serve命令时使用--watch标志。例如，要以启用自动重建的方式运行jekyll serve，您需要运行以下命令：
```
jekyll serve --watch
```
一旦您启用了自动重建，您对源文件的任何更改都将会自动反映在您的站点中。

以下是使用自动重建的一些好处：

您可以在实时中看到您的更改。
您在更改后无需手动重新构建您的站点。
这可以节省您的时间和麻烦。
如果您没有使用自动重建，您需要在更改后手动重新构建您的站点。要执行此操作，您可以运行`jekyll build`命令。

