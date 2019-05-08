---
layout: post
title:  "Windows上使用jekyll+github搭建免费博客"
date:   2019-05-08 09:47:03 +0800
categories: jekyll update
---

## **jekyll+github搭建个人博客** 

##### （一）下载Ruby 
##### （二）安装jekyll
##### （三）开启jekyll服务器 
##### （四）使用github展示博客 

#### **一、下载Ruby**
 
Ruby，一种简单快捷的面向对象（面向对象程序设计）脚本语言，安装Jekyll需要电脑上安装Ruby：

 + window系统下，可以使用rails install来安装ruby环境，[下载地址](http://rubyinstaller.org/downloads/) ，建议下载2.3以上的新版。
 + 下载 RailsInstaller 之后，双击 railsinstaller-3.2.0 文件，启动 Ruby 安装向导点击next，向导完成安装，记得勾选 Add Ruby executables to your PATH，直到 Ruby 安装程序完成 Ruby 安装为止
 + 安装后，在cmd中输入ruby -v和gem -v来看看是否安装成功，看到版本号就说明成功。

**注意：用RubyInstaller安装Ruby之后都附带有Gems。**

#### **二、安装jekyll**
jekyll是一个简单的免费的Blog生成工具，类似WordPress。但是和WordPress又有很大的不同，原因是jekyll只是一个生成静态网页的工具，不需要数据库支持。但是可以配合第三方服务,例如Disqus。最关键的是jekyll可以免费部署在Github上，而且可以绑定自己的域名。

**使用gem安装jekyll**，在命令行输入

    gem install jekyll

所有的jekyll的gem依赖包都会被自动安装。

**下载bundler**，命令行输入

    gem install bundler

**建立自己的第一个博客**

    cd d:  // 我的博客建立在d盘

    jekyll new youBlogFileName   // youBlogFileName为我的博客文件名

#### **三、开启jekyll服务器**

    cd youBlogFileName  // 一定要进入创建的blog目录，否则服务无法开启

    jekyll serve  // 开启服务器

jekyll服务器的默认端口是4000，所以打开浏览器http://localhost:4000 就可以看到生成的博客页面

**使用jekyll写博客**

在博客文件中的posts中写博客文件

#### **四、使用github展示博客**

+ 创建个人仓库
  就是建立一个新的仓库，但是这个仓库的名字必须为你的github的名字+github+io，即yourname.github.io

+ 将目录切换到你想要放github博客的文件目录下，在这个目录git bash 将刚才建的仓库克隆下来：

    git clone git@github.com:yourname/yourname.github.io.git

  这时，你会发现你的文件夹下会多出一个yourname的文件，我们把之前的blog下的所有文件复制到里面。

+ 然后把里面的所有文件push到刚刚建的远程仓库，步骤我就不写了。
  这时，在浏览器里面输入网址：http://yourname.github.io 就可以看你的个人博客网站了，这就是你的博客网站的地址了。
  **前面所说的yourname指的是你的github账号名字。**