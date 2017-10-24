---
layout: default
title:  "CSS Flex Learn!"
date:   2017-10-22 14:19:40 +0800
categories: jekyll update
---
## CSS Flex Learn---弹性布局---垂直居中的简易解决方案
参考至：
[1、阮一峰flex布局：语法篇;](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
[2、阮一峰flex布局：实战篇;](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

### 【一】、任何容器都可以设为flex，(display:flex;)，容器设为flex，其子元素的float、clear、vertical-align失效；行内元素也可设为flex，(display:inline-flex),且flex可嵌套使用；Webkit内核的浏览器，必须加上-webkit前缀。

### 【二】、有主轴与纵轴之说；

### 【三】、有六个容器属性：

####  【1】flex-direction:决定主轴的方向;
---【row：横轴,row-reverse：横轴逆向,column：竖行，column-reverse：竖行逆向】；
####  【2】flex-wrap:是否换行;
---【wrap：换行，nowrap：不换行，wrap-reverse换行，但第一行显示在下方，】
#### 【3】flex-flow：flex-direction+flex-wrap；
#### 【4】justify-content：项目在主轴上的对齐方式;
---【flex-start：主轴开始对齐，flex-end:主轴逆向对齐，center：主轴中间对齐，space-between：相邻项目之间的距离相等，space-around：项目主轴前后距离相等，故项目之间的距离比项目与边界距离宽1倍】;
#### 【5】align-items：项目在纵轴上的对齐方式；
---【flex-start、flex-end、center、baseline：项目的第一行文字的基线对齐，stretch：如果项目未设置高度或设为auto，将占满整个容器的高度】
#### 【6】align-content：多行的对齐方式;
--- 【flex-start,flex-end,center,space-between,space-around,strtch】

### 【四】、有六个项目属性：
#### 【1】order--定义项目在主轴上的排列顺序，默认从0开始，值越小，越靠前；
#### 【2】flex-grow--主轴剩余空间的放大比例，默认为0不放大；
#### 【3】flex-shrink--主轴空间不足时的缩放比例，默认为1 ；
#### 【4】flex-basis--缩放前占主轴的空间大小--auto，项目本来大小；
#### 【5】flex：(flex-grow)+(flex-shrink)+(flex-basis);
#### 【6】align-self：纵轴对齐方式默认auto为stretch，与align-items类似；


### 【五】、经典布局----实现在webDemo中可查看

#### 【1】固定的底栏；
#### 【2】圣杯布局；
#### 【3】基本网格布局；
#### 【4】悬挂式布局；
#### 【5】流式布局；
#### 【6】输入框布局；
#### 【7】骰子的布局；
