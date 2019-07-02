---
layout: post
title:  "Win10使用VMWare15安装Ubuntu-18.04.2-desktop-amd64"
date:   2019-07-02 10:50:08 +0800
categories: jekyll update
---

#### 本文在Win10系统中使用VMWare Workstation Pro 15.1.0虚拟机安装Ubuntu-18.04.2-desktop-amd64.iso系统，同时安装VMWare Tools(实现ubuntu界面与win10系统桌面之间的文件拷贝)。

#### 一、前提

* 1、win10 X64
* 2、虚拟机 [VMWare Workstation Pro详解](https://www.vmware.com/cn/products/workstation-pro/faqs.html)
* 3、linux发布版本Ubuntu的镜像文件（Ubuntu-18.04.2-desktop-amd64.iso）

#### 二、相关下载

* 1、[虚拟机VMWare Workstation Pro 15.1.0发布下载](https://my.vmware.com/web/vmware/details?downloadGroup=WKST-1510-WIN&productId=799&rPId=33369)
* 2、[Ubuntu 18.04.2 镜像文件](https://ubuntu.com/download/desktop)


#### 三、安装虚拟机（VMWare Workstation Pro 15.1.0）：几乎一直是下一步 
* 1、注意安装位置（不要选在C盘）;
* 2、尽量不选择更新【取消打钩】；
* 4、许可证密钥--百度上网找；

#### 四、新建虚拟机、安装镜像文件

* 【1】 打开虚拟机、选择新建【典型】进行相关配置

![新建虚拟机](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/create_virtua_machine.png)

* 【2】选择稍后安装操作系统

![稍后安装操作系统](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/next.png)

* 【3】选择linux

![linux](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/linux.png)

* 【4】根据需要修改安装路径（最好不要选择C盘）

![选择安装路径](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/install_address.png)

* 【5】根据需要设置最大磁盘大小，选择 将虚拟机磁盘存储为单个文件

![虚拟磁盘存储为单个文件](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/single_file.png)

* 【6】点击自定义硬盘

![自定义硬盘你](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/custom.png)

* 【7】设置虚拟机内存

![设置虚拟机内存](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/memory.png)

* 【8】设置处理机内核数

![虚拟机内核数](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/cpu.png)

* 【9】配置需使用的ISO镜像文件

![ISO镜像文件](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/iso.png)

* 【10】配置完，点击启动虚拟机

![启动虚拟机](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/start.png)

* 【11】选择安装语言，点击安装Ubuntu

![安装Ubuntu](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/install.png)

* 【12】默认选项，点击继续

![继续](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/install_01.png)

* 【13】默认选项，点击现在安装  【注：这里选择 清除整个磁盘并安装Ubuntu 不会对安装路径所在的磁盘的其他文件造成影响】

![清除整个磁盘并安装ubuntu](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/install_02.png)

![清除整个磁盘并安装ubuntu](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/install_03.png)

* 【14】输入地址信息

![地址信息](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/install_04.png)

* 【15】设置个人及登录信息

![设置登录信息](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/install_05.png)

* 【16】安装完成后，选择重启即可---至此，Ubuntu18.04.2 desktop便可以正常使用了

![重启](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/install_06.png)

![虚拟机界面](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/install_07.png)

#### 五、安装VMWare Tools---解决以下问题

* 因为Ubuntu18.04.2界面不是全屏的，即使点击全屏展示也无用
* 虚拟机和win10系统之间无法直接拷贝文件

* 【1】选择虚拟机-管理-安装VMWare Tools

![选择安装](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/tools_00.png)

* 【2】完成后打开文件目录，下方会显示VMWare Tools的安装光盘

![安装光盘](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/tools_01.png)

* 【3】复制步骤2中的以tar.gz结尾的压缩文件至主目录，然后通过右键提取，之后便可获得一个如图所示的文件夹

![右键提取](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/tools_02.png)

* 【4】 点击桌面左下角的省略号、出现终端点击打开，进入到vmware-install.pl文件所在的目录，执行以下命令进行安装 [sudo  ./vmware-install.pl]
【注：脚本执行过程中，会有很多询问想，首次询问是否安装时输入yes，之后一直回车执行即可】

![脚本执行](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/tools_03.png)

* 【5】安装完成后，会显示如下界面。重启虚拟机，即可实现虚拟机和Win10界面的文件互相拷贝.

![重启虚拟机](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/win10_vmware_ubuntu/tools_04.png)


#### OVER！