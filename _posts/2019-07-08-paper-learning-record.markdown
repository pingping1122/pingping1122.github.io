---
layout: post
title:  "201905-06-paper-learnig-record"
date:   2019-07-08 16:50:08 +0800
categories: jekyll update
---

**导师建议：【在读论文时重点关注它的核心创新点，
即它提出的方案和此前的各类方案相比有什么关键性的差异，以及“在什么场景下”、“通过什么原理”能取得更好的效果。
这样通过读一篇论文，可以了解它的related work、references，并逐渐把知识体系建立起来。】**

#### 一、HPCA:《Plaint：Leveraging Approximation to Improve Datacenter Resource Efficiency》  

**导师评语：Plaint的核心思路还是比较主流的，尤其是在当前机器学习类应用十分流行的环境下。之前还见过有的论文讨论视频类应用，通过自动动态调整视频的清晰度，也可以实现高帧率和高利用率。思路应该是很类似的。**

[论文地址](https://ieeexplore.ieee.org/document/8675193)

* Pliant，一种在线云运行时系统，利用近似计算应用程序的特性来容忍输出质量上的损失，从而实现高QoS和高利用率。
* 方法：与以往集群调度程序降低某些应用程序优先级不同。Pliant由用户向其调度器提供应用程序可容忍的不精确阙值，Pliant实现在不超过此阙值的情况下动态调整近似值，以达到满足交互服务QoS所需的最小值。


#### 二、HPCA:《Poly:Efficient Heterogeneous System and Application Management for Interactive Applications》

[论文地址](https://dblp.uni-trier.de/db/conf/hpca/hpca2019.html)

* 【1】	基础知识：OpenCL编程--（不仅可以在任何兼容硬件上运行，而且可以针对不同的设备完成一次编译，这些设备甚至不需要有相同的体系结构，或是来自同一个厂商），数据中心的硬件加速、尾延迟、Qos敏感的工作负载（一般为运行在云上的交互式应用程序，存在延迟松弛），99thpercentile响应延迟等； 
* 【2】	Poly：基于OpenCL的异构系统优化框架，利用数据中心内基于GPU和FPGA的加速器，在保证Qos的同时，提高总体的吞吐量和能效；
 * （1）	编译时：静态内核分析---从并行模式级别到操作符级别分层分析每个内核---输出是一个OpenCL内核设计空间；
 * （2）	运行时：动态内核调度---由系统监控器、模型和优化器三部分组成，利用监视器输出的工作负载，poly利用延迟松弛，选择正确的内核调度到平台。----方法：通过对具有较短延迟的就绪内核进行优化排序来近似模拟应用程序的最优延迟。
 * （3）	细粒度的设计空间：利用数据中心叶子节点的异构体系结构。



