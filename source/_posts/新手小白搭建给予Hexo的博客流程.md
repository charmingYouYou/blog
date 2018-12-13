---
title: 新手小白搭建基于Hexo的博客流程
auth: charmingYouYou
categories: 
- 博客
tags: 
- hexo
- 域名
- github Page
- markDown
---
# 新手小白搭建基于Hexo的博客流程

>

## 初始准备工具

 * [安装git](https://git-scm.com/downloads)
 * [安装nodeJs](https://github.com/blinkfox/typora-vue-theme.git)

## 安装git(以win为例, mac下请使用终端)

1. [window下安装git教程](https://jingyan.baidu.com/article/90895e0fb3495f64ed6b0b50.html)  [mac下安装git教程](https://jingyan.baidu.com/article/2a138328d0df4f074a134fc1.html)

2. git 安装完成后，在桌面鼠标右键点击`git bash here`

   ![git-bash-here](https://charmingyouyou-1256314320.picbj.myqcloud.com/blog/hexo_1.png)

3. 在打开的终端中输入以下信息`git --version` `node -v` `npm -v`来判断git和node是否安装成功

   ![hexo_2](https://charmingyouyou-1256314320.picbj.myqcloud.com/blog/hexo_2.png)

4. 在以上指令都显示对应版本号后, 我们的初始准备工作就告一段落了, 接下来就可以正式开始搭建我们的第一个博客了~

> Tip:  对于想详细了解git和node的同学可以去以下地址学习更多哦~
>
> 1. [git入门教程](https://charmingyouyou-1256314320.picbj.myqcloud.com/blog/hexo_1.png)
> 2.  [node官方文档](http://nodejs.cn/api/)



## Hexo

> Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

* ##### [官方文档](https://hexo.io/zh-cn/)

* ##### 安装Hexo

  在准备放置博客的文件夹下执行`git bash here`打开终端后执行`npm install -g hexo-cli --registry=https://registry.npm.taobao.org`(mac用户请在root下执行该语句)

![hexo安装成功](https://user-gold-cdn.xitu.io/2018/1/20/161117c728dda55c?imageView2/0/w/1280/h/960/)

* ##### 初始化hexo
