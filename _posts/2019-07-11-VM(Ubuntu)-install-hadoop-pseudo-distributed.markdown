---
layout: post
title:  "虚拟机Ubuntu(18.04.2)下安装配置Hadoop(2.9.2)(伪分布式+Java8)"
date:   2019-07-11 10:50:08 +0800
categories: jekyll update
---

#### **【本文结构】**

* 【1】安装Hadoop前的准备工作
   * 【1.1】 创建新用户
   * 【1.2】 更新APT
   * 【1.3】 安装SSH
   * 【1.4】 安装Java环境
* 【2】安装和配置hadoop
   * 【2.1】 Hadoop下载
   * 【2.2】 Hadoop伪分布式配置

#### **【踩过的坑】**

* 【1】 需要**在Java8上安装Hadoop**,开始用Java11一直失败；
* 【2】 一定要再熟悉大致流程后再安装，专注于一篇笔记的同时参考其他笔记。
* 【3】 本文参考笔记
   * 【1.1】 [Ubuntu16.04 下 Hadoop的安装与配置（伪分布式环境）](https://www.cnblogs.com/87hbteo/p/7606012.html)
   * 【1.2】 [Ubuntu虚拟机下的Hadoop伪分布式集群搭建 ](https://www.cnblogs.com/sdwyz/p/10797820.html)
   * 【1.3】 [在Ubuntu下安装和搭建Hadoop环境(伪分布式环境)](https://www.jianshu.com/p/7905e0763a3d)

#### **【所需下载的文件】**
* 【1】 [JDK--Java8环境](https://www.oracle.com/technetwork/java/javase/downloads/index.html)
* 【2】 [Apache Hadoop2.9.2](https://www.apache.org/dyn/closer.cgi/hadoop/common/hadoop-2.9.2/hadoop-2.9.2.tar.gz)

#### **【其他知识点】**
* 【1】 查看本机ip 
    
        sudo apt install net-tools
        ifconfig                     # 查看虚拟机Ip

* 【2】 VIM命令

        vi filename    # 进入文件
        insert键       # 编辑文本
        esc键          # 退出编辑
        :wq            # 退出并保存
        ctrl+s         # 锁屏
        ctrl+q         # 解锁
        fi             # 文件结尾标识

-------------------------------------------------------------------------------------------------------------------------------------
<br/>

#### **【1】安装hadoop前的准备**

* **【1.1】 创建Hadoop用户**

&emsp; &emsp; 为了方便以后的实验进行，推荐创建一个新的Hadoop用户，所有的实验内容都登录该用户进行，具体的shell代码和注释如下：


      $ sudo useradd -m hadoop -s /bin/bash      # 创建hadoop用户，并使用/bin/bash 作为shell
      $ sudo passwd hadoop                       # 为hadoop用户设置密码，之后需要连续输入两次密码
      $ sudo adduser hadoop sudo                 # 为hadoop用户添加管理员权限
      $ su - hadoop                              # 切换当前用户为hadoop
 


* **【1.2】更新apt**

&emsp; &emsp; APT是一款软件管理工具，Linux采用APT来安装和管理各种软件，安装成功Linux系统以后，需要及时更新APT软件，否则后序的一些软件可能无法正常安装，更新APT使用以下命令：

     $ sudo apt-get update                      # 更新hadoop用户的apt，方便后面的安装   

* **【1.3】安装SSH,设置SSH无密码登录**

&emsp; &emsp;SSH是Secure Shell的缩写，

&emsp; &emsp;**<font color="red">为什么安装hadoop之前需要配置SSH呢？</font>** 这是因为Hadoop名称节点(NameNode) 需要启动集群中所有机器的Hadoop守护进程，这个过程需要通过SSH登录来实现。Hadoop并没有提供SSH输入密码登录的形式，因此，为了能够顺利登录集群中的每台机器，需要将所有机器配置为“名称节点可以无密码登录它们”

&emsp; &emsp;Ubuntu默认已安装SSH客户端，故只需要安装SSH服务器，在终端执行以下命令：

      $ sudo apt-get install openssh-server     # 安装ssh服务器

&emsp; &emsp; 然后可以使用如下命令登录本机（因为是伪分布式集群，只有一台机器，同时作为名称节点和普通节点），如果提示输入密码，则表示安装成功了。

      $ ssh localhost                           # 登录ssh，第一次登录输入yes  或者让输入密码直接两次回车


![第一次登录ssh](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/000.png)


&emsp; &emsp;由于这样登录需要每次输入密码，所以，需要配置SSH为无密码登录，这样在hadoop集群中，名称节点要登录某台机器就不需要人工输入密码了。

      $ cd ~/.ssh                               # 切换目录
      $ ssh-keygen -t rsa                       # 会有提示，按enter即可（即不设置密码），这条语句生成公钥和私钥两个文件
      $ cat ./id_rsa.pub >> ./authorized_keys   # 加入授权，cat file1 >> file2 的含义是将file1的内容写到file2尾部
      $ ssh localhost                           # 此次再登录ssh，无需输入密码即可。


![生成公钥私钥](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/001.png)


![无密登录ssh](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/002.png)


* **【1.4安装Java环境】**

&emsp; &emsp;Hadoop是基于Java环境开发的，同时Java语言也可以用来编写Hadoop应用程序，在Linux系统中安装Java环境有两种方式：Oracle的JDK和openJdk,本文采用第一种：

&emsp; &emsp;首先在Oracle官网下载JDK1.8,接下来安装并配置。这里选择的是(jdk-8u211-linux-x64.tar.gz)

&emsp; &emsp;**<font color="red">注意是usr !!! 不是user </font>**

     $ mkdir /usr/lib/jvm                                          # 创建jvm文件夹
       # 解压到/usr/lib/jvm目录下(因为压缩包在在桌面放着)
     $ sudo tar zxvf /home/root123456/桌面/jdk-8u211-linux-x64.tar.gz -C /usr/lib/jvm          
     $ cd usr/lib/jvm                                              # 进入usr/lib/jvm目录
     $ mv jdk1.8.0_211 java                                        # 将jdk1.8.0_211重命名为java  此步可能权限不够，在其前加上sudo


![解压jdk压缩包](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/003.png)


![文件重命名权限不够](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/004.png)


     $ vi ~/.bashrc                           # 给JDK配置环境变量

&emsp; &emsp;编辑.bashrc文件，添加如下指令：

     export JAVA_HOME=/usr/lib/jvm/java
     export JRE_HOME=${JAVA_HOME}/jre
     export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib
     export PATH=${JAVA_HOME}/bin:$PATH

&emsp; &emsp;文件修改完毕后，输入以下代码：

     $ source ~/.bashrc                       # 使新配置的环境变量生效
     $ java -version                          # 检测是否安装成功，查看java版本       


![java环境配置检查](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/005.png)


&emsp; &emsp;java安装成功后，就可以进行Hadoop的安装了。

--------------------------------------------------------------------------------------------------------------------------------------
<br/>

#### **【2】安装配置Hadoop**

* **【2.1】Hadoop的下载安装**

&emsp; &emsp; 我的虚拟机Ubuntu安装了VMWare Tools，可以在win10桌面和Ubuntu桌面之间直接交换文件。所以在apache hadoop上直接下载的文件之后拷贝到Ubuntu桌面上。

      #解压到/usr/local目录下
     $ sudo tar -zxvf /home/root123456/桌面/hadoop-2.9.2.tar.gz -C  /usr/local     
     $ cd /usr/local                          # 切换目录值
     $ sudo mv hadoop-2.9.2 hadoop            # 重命名为hadoop
     $ sudo chown -R hadoop ./hadoop          # 修改文件权限

&emsp; &emsp; 给hadoop配置环境变量，

     vi /.bashrc

&emsp; &emsp; 将下面的代码添加到.bashrc文件中:

     export HADOOP_HOME=/usr/local/hadoop
     export CLASSPATH=$($HADOOP_HOME/bin/hadoop classpath):$CLASSPATH
     export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
     export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

&emsp; &emsp;配置完后，执行source ~/.bashrc使设置生效，并查看hadoop是否安装成功。


![Hadoop安装完成](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/005-1.png)

* **【2.2】伪分布式配置**

&emsp; &emsp;Hadoop的默认模式即为本地模式(即单机模式),无需配置就可以运行，值得注意的是，Hadoop的模式变更(单机模式、伪分布式、分布式)完全是通过修改配置文件实现的。

&emsp; &emsp;这里配置的是伪分布式模式，即只有一个节点(一台机器),这个节点既作为名称节点(NameNode)，也作为数据节点(DataNode)，伪分布式模式配置涉及三个配置文件： hadoop目录/etc/hadoop/下的hadoop-env.sh、core-site.xml 和 hdfs-site.xml ：

&emsp; &emsp;【2.2.1】首先将jdk1.8的路径添加到/etc/hadoop/hadoop-env.sh文件中

     export JAVA_HOME=/usr/lib/jvm/java

&emsp; &emsp;【2.2.2】在core-site.xml文件中增加

    <configuration>
        <property>
             <name>hadoop.tmp.dir</name>
             <value>file:/usr/local/hadoop/tmp</value>
             <description>Abase for other temporary directories.</description>
        </property>
        <property>
             <name>fs.defaultFS</name>
             <value>hdfs://localhost:9000</value>
        </property>
    </configuration>

&emsp; &emsp;【2.2.3】在hdfs-site.xml文件中增加

     <configuration>
        <property>
             <name>dfs.replication</name>
             <value>1</value>
        </property>
        <property>
             <name>dfs.namenode.name.dir</name>
             <value>file:/usr/local/hadoop/tmp/dfs/name</value>
        </property>
        <property>
             <name>dfs.datanode.data.dir</name>
             <value>file:/usr/local/hadoop/tmp/dfs/data</value>
        </property>
      </configuration>



![Hadoop伪分布式配置](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/009.png)


&emsp; &emsp;Hadoop的运行方式是由配置文件决定的(运行Hadoop时会读取配置文件)，因此如果需要从伪分布式切换为单机模式，需要删除core-site.xml中的配置项。

&emsp; &emsp;伪分布式虽然只需要配置fs.defaultFS和dfs.replication就可以运行，不过若没有配置hadoop.tmp.dir参数，则默认使用的临时目录为/temp/hadoop-hadoop，而这个目录在重启时有可能被系统清理掉，导致必须重新执行format才行。同时我们也指定了dfs.namenode.name.dir和dfs.datanode.data.dir，否则在接下来的步骤中可能会出错。

&emsp; &emsp;配置完成后，执行NameNode的格式化

     $ ./bin/hdfs namenode -format

&emsp; &emsp; 启动namanode和datanode进程

&emsp; &emsp; 启动完后，可以通过jps来判断是否成功启动，若成功，则会出现以下四个进程“NameNode”、”DataNode” 和 “SecondaryNameNode” 

     $ ./sbin/start-dfs.sh
     $ jps

![Hadoop格式化1](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/009.png)

![Hadoop格式化2](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/009-1.png)

![Hadoop启动namanode和datanode](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/010.png)


&emsp; &emsp;成功启动后，可以通过web界面 http://localhost:50070 查看NameNode 和 Datanode 信息，还可以在线查看 HDFS 中的文件。 

![web界面50070](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/VM_ubuntu_install_hadoop/011.png)


&emsp; &emsp;至此，Hadoop的伪分布式部署已完成啦！需要使用YARN的话，还需要单独配置mapred-site.xml和yarn-site.xml文件。