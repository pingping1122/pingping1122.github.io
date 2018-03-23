---
layout: post
title:  "linux 常见命令+GIT简单解释"
date:   2017-12-04 13:49:20 +0800
categories: jekyll update
---

### linux常见命令 

* #### 【1】cd--切换当前目录(绝对路径或相对路径);
* #### 【2】ls--查看文件与目录;
* #### 【3】grep--分析一行信息：
   * ##### grep [-c/-i] '查找字符串' filename; 
   * ##### -c 计算找到‘查找字符串’的次数;
   * ##### -i 忽略大小写;
* #### 【4】find--查找;
   * ##### find [path] [option] [action];
   * ##### eg.find \root -mtime 0   在当前目录下查找今天之内有改动的文件;
* #### 【5】cp--(copy)复制文件;
* #### 【6】mv--(move)移动文件;
   * #####  mv file1 file2 dir  将文件file1和file2移动至dir;
* #### 【7】rm--(remove)用于删除文件或目录;
* #### 【8】ps--(process)用于将某个时间点的进程运行情况选取下来并输出;
* #### 【9】kill、killall
* ##### 【10】file--用于判断某个文件的基本数据类型(在linux下文件的类型并不是以后缀名来分的);
   * ##### file filename
* #### 【11】tar--用于对文件进行打包
   * ##### 压缩：tar -jcv -f  taredFile taringFile;
   * ##### 查询: tar -jtv -f taredFile;
   * ##### 解压: tar -jxv -f taredFile -C 预解压的文件目录;
* #### 【12】cat--查看文本文件的内容;
* #### 【13】chgrp--改变文件所属用户组;
* #### 【14】chown--改变文件的所有者;
* #### 【15】chmod--改变文件的权限;
* #### 【16】vim--文件编辑;
* #### 【17】gcc--用于将C语言的源程序文件编译成可执行程序;
* #### 【18】time--用于测算一个命令（即程序）的执行时间;

### GIT简单解析

![git--协作原理](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/git/git.png)

* #### 本地数据库创建方式
  * ##### 直创本地：文件夹下 git init
  * ##### 从远程克隆： git clone sshPath 

* #### 提交信息要认真填写，提交点commit--40位英文数字命名；

发生冲突时：

     \<\<\<\<\<\<\<\<\< HEAD
     AAAAAAAAA-----AAAA为本地数据库的内容;
     ===========
     BBBBBBBBB-----BBBB为远程数据库内容;
     \>\>\>\>\>\>\>\>\>

* #### 本地创建数据库 
  * ##### git init
  * ##### git add file\
  * ##### git commit -m 'first commit'
* #### 本地创建并切换分支 git checkout -b develop
  * ##### git branch develop
  * ##### git checkout develop 
* #### 合并分支
  * ##### git checkout master
  * ##### git merge develop
* ####  删除分支
  * ##### git branch -d develop
* #### 推送本地数据库到远程
  * ##### github 上传建test仓库
  * ##### git remote add origin (sshPath of test仓库)
  * ##### git push -u origin master


