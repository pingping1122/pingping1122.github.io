---
layout: default
title:  "利用Jekyll和Github搭建免费的个人blog"
date:   2017-08-08 16:01:20 +0800
categories: jekyll update
---
## 本文参考自大漠穷秋的原文章

[利用Jekyll和Github搭建免费的个人blog---大漠穷秋](https://damoqiongqiu.github.io/)

### 一、安装git和小乌龟+注册github账号并创建项目---直接参考大漠老师的即可
### 二、安装配置Jekyll-----jekyll是基于Ruby开发的，故需先安装Ruby和RubyGems

### windows下使用第三方安装工具rubyinstaller安装ruby

[rubyinstaller下载](https://rubyinstaller.org/downloads/)

[菜鸟教程--rubyinstaller安装ruby](http://www.runoob.com/ruby/ruby-installation-windows.html)

### 具体安装步骤如下：

    Window 系统下，我们可以使用 RubyInstaller 来安装 Ruby 环境，下载地址为：请点击这里下载。
    下载 rubyinstaller 之后，解压到新创建的目录下：
    双击 rubyinstaller-2.2.3.exe 文件，启动 Ruby 安装向导。
    点击 Next，继续向导，记得勾选 Add Ruby executables to your PATH，直到 Ruby 安装程序完成 Ruby 安装为止。


[RubyGems下载](https://rubygems.org/pages/download/) 

[RubyGems解压使用](http://www.runoob.com/ruby/ruby-rubygems.html)

[使用sublime安装markdown插件](http://blog.csdn.net/ababybear/article/details/51512125)

### 三、提交第一篇文章

【1】在mgblog的_posts目录里面新建一个普通的文件，
命名类似 2017-07-04-welcome-to-jekyll.markdown
注意文件名，
Jekyll对文件名有自己的要求，所以我们必须采用上面这种方式来命名，
里面尤其不要带有非英文字符和特殊字符。在你的代码编辑器里面打开新文件，删掉所有内容，
然后把以下内容粘贴进去：

---

layout: post

title:  "利用Jekyll和Github搭建免费的个人博客"

date:   2017-08-08 16:01:20 +0800

categories: jekyll update


---


【2】按照markdown格式书写文件即可；--markdow添加图片链接时需要使用RAW地址。

【3】将本地jekyll服务器启动起来看看效果；

cd mgblog

bundle exec jekyll serve

起来之后，打开浏览器，访问http://localhost:4000 ,可以在看到该篇文章即可；

【4】ok之后，将你的文章push到github上即可。

【5】push完之后，看就可以在 http://你在github上的用户名.github.io  上看到与本地一样的内容了；