---
layout: post
title:  "Win10环境下Hadoop(单节点伪分布式)的安装与配置--bug(yarn的8088端口打不开+)"
date:   2019-07-06 10:50:08 +0800
categories: jekyll update
---

#### **一、本文思路**

* 【1】、配置java环境--JDK12（Hadoop的底层实现语言是java,hadoop运行需要JDK环境）
* 【2】、安装Hadoop
   * 1、解压hadop
   * 2、配置hadoop环境变量
   * 3、配置Hadoop文件

#### **二、所需下载文件**

* 【1】[JDK下载地址](https://www.oracle.com/technetwork/java/javase/downloads/index.html)


![选择基础版本下载](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/jdk_00.png)


* 【2】[Hadoop下载地址---推荐binary版本是提前编译好的](https://hadoop.apache.org/releases.html)


![选择binary下载](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/hadoop_binary.png)


* 【3】[hadoop在windows上运行需要winutils支持和hadoop.dll等文件](https://github.com/steveloughran/winutils)
   
   * 在github仓库中找到对应版本的二进制库hadoop.dll和winutils.exe文件，然后把文件拷贝到hadoop解压的bin目录中去
   * 【目前未找到对应的2.9.2版本，这一步未操作】


#### **三、基础知识**
* 【1】 Apache Hadoop系统的两个核心组件
    * （1）用于存储数据的Hadoop分布式文件系统（HDFS）
    * （2）用于实现数据处理的应用程序的Hadoop Yarn

#### **四、JDK12安装配置过程**

##### 【1】JDK与JRE比较

* JDK:java安装工具包，包含JRE。因此只需下载JDK即可；
* JRE:java运行环境，用来运行JAVA程序的。

##### 【2】JDK安装---选择默认安装目录即可。

##### 【3】JDK配置--系统变量

* (1)新建JAVA_HOME变量，变量值填写JDK的安装目录（我的是默认安装环境 C:\Program Files\Java\jdk-12.0.1）。


![新建javahome变量](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/java_home.png)


* (2)新建CLASSPATH变量，变量值  .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar  (注意前面有一个点)。

**此处注意不要使用相对路径JAVA_HOME，因为重启电脑后cmd执行javac会失败**


![新建classpath变量](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/class_path.png)


更改为：


![新建classpath变量](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/classpath.png)


* (3)在path变量值后加  %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

**此处注意不要使用相对路径JAVA_HOME，因为重启电脑后cmd执行javac会失败**


![path后新增jdk路径](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/path_add_jdk.png)


更改为：


![path后新增jdk路径](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/path_jdk.png)


* (4)此处注意的是jdk安装目录下是没有jre的，需要手动添加**   
  * 1、打开cmd
  * 2、切换至jdk安装目录下 （我的是：C:\Program Files\Java\jdk-12.0.1）
  * 3、执行 bin\jlink.exe --module-path jmods --add-modules java.desktop --output jre 
  * 4、结果如下图，在C:\Program Files\Java\jdk-12.0.1下出现jre即可。


![path新增jdk路径](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/jdk_jre.png)


![path新增jdk路径后的编辑文本样式](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/path_jdk_result.png)


* (5)检查是否配置成功，运行cmd，分别输入java, javac, java -version 三个都可执行即为安装配置成功。

#### **五、Hadoop2.9.5安装配置过程**

##### 【1】Hadoop安装---下载的安装包直接解压即可（我的在 D:\Hadoop\hadoop-2.9.2 目录）


![hadoop安装目录](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/hadoop_install_path.png)


##### 【2】Hadoop环境配置---系统变量

* (1)新建HADOOP_HOME变量，变量值D:\Hadoop\hadoop-2.9.2  


![新建HADOOP_HOME变量](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/hadoop_home.png)


* (2)在path变量值后添加 %HADOOP_HOME%\bin; 


![新建HADOOP_HOME变量](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/hadoop_path.png)


* （3）此时测试hadoop是否安装成功会失败：原因是**jdk的JAVA_HOME环境变量的配置路径不能有空格**(C:\Program Files\Java\jdk-12.0.1),将其中的 **Program Files 替换为 PROGRA~1**即可。


![java_home有空格](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/space.png)


将其中的 **Program Files 替换为 PROGRA~1**即可


![java_home无空格](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/no_space.png)


**cmd下执行 hadoop version成功，说明hadoop环境配置成功。**

##### 【3】 Hadoop伪分布式文件配置

* (1)在hadoop根目录下新建文件夹data,然后在其下创建另个子文件夹datanode和namenode


![新建data文件夹](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/hadoop_file_00.png)


![data下新建文件夹](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/hadoop_file_01.png)


* (2)确认 ../etc/hadoop/core-site.xml中有如下代码

core-site.xml代码：
     
     <configuration>
      <!--fs.defaultFS属性，为NameNode（HDFS元数据的服务器）指定主机名和请求端口号 -->
       <property>
         <name>fs.defaultFS</name>
         <value>hdfs://localhost:9000</value>
       </property>
     </configuration>

* (3)确认../etc/hadoop/mapred-site.xml （如不存在该文件，则将mapred-site.xml.template文件更改为mapred-site.xml）中有如下代码：

mapred-site.xml代码：

     <configuration>
     <!-- 为MapReduce指定框架名，值为Yarn，告知Mapreduce它将作为Yarn的应用程序运行 -->
      <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
      </property>
     </configuration>

* (4) 确认../etc/hadoop/hdfs-site.xml中有如下代码 （namenode和datanode是（1）中新建文件的地址）

hdfs-site.xml代码：---cuowu 

     <configuration>
     <!-- hdfs默认为系统文件系统中的每个文件保存3份副本，以作冗余备份，单机版hadoop没有备份需要，设置dfs.replication为1 -->
       <property>
          <name>dfs.replication</name>
          <value>1</value>
       </property>
       <!-- 此处直接用window下的地址 D:\Hadoop\hadoop-2.9.2\data\namenode 会报错，应改为正斜杠，且磁盘名称前也需要一个正斜杠 -->
       <property>
         <name>dfs.namenode.name.dir</name>
         <value>/D:/Hadoop/hadoop-2.9.2/data/namenode</value>
       </property>
       <property>
         <name>dfs.datanode.data.dir</name>
         <value>/D:/Hadoop/hadoop-2.9.2/data/datanode</value>
      </property>
    </configuration>

* (5)确认../etc/hadoop/yarn-site.xml中有如下代码

yarn-site.xml代码：
     
      <configuration>
       <!-- 属性yarn.nodemanager.aux-services告诉NodeManager需要实现一个名为 mapreduce.shuffle的辅助服务-->
        <property>
          <name>yarn.nodemanager.aux-services</name>
          <value>mapreduce_shuffle</value>
        </property>
        <property>
          <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
          <value>org.apache.hadoop.mapred.ShuffleHandler</value>
        </property>
      </configuration>


* (6) ../etc/hadoop/hadoop-env.cmd（修改JDK的安装路径)


![javahome路径完善](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/hadoop_file_02.png)


* (7)格式化HDFS文件系统（节点格式化），通过cmd进入文件夹 D:\Hadoop\hadoop-2.9.2\bin

后运行
   
       hdfs namenode -format

执行成功结果：


![节点格式化成功](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/hadoop_file_04.png)


然后进入sbin文件输入：start-all.cmd  之后会有四个窗口跳出来,分别是
    * Hadoop Namenode
    * Hadoop datanode
    * YARN Resource Manager
    * YARN Node Manager

* (8)hadoop自带的web控制台GUI
 
 * 资源管理GUI(yarn的web界面) : http://localhost:8088 


 ![yarn的web界面打不开](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/yarn_fail.png)


 * 节点管理GUI(hdfs的web界面)： http://localhost:50070


 ![hdfs的web界面](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/hdfs_ok.png)



#### **六、我的问题**

**五中步骤(7)中格式化hdfs、再输入start-all命令后只出现两个窗口，关于Yarn部分的窗口出现error，http://localhost:8088界面打不开**


![start-all yarn失败](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_install_local_mode_hadoop/fail.png)

