---
layout: post
title:  "CSS Grid Layout小结"
date:   2017-12-05 15:10:20 +0800
categories: jekyll update
---

### CSS Grid布局：

* #### 【1】使chrome支持调试grid layout
  * ##### 则在chrome地址栏输入:
    chrome://flags#enable-experimental-web-platform-features
  * ##### 回车---点击enable---再重启chrome即可；
* #### 【2】css_grid主要由两部分组成
  * ##### wrapper父元素--实际的grid网格；
  * ##### items子元素--grid网格的内容；
  * ##### .wrapper{
            display:grid;
            }
* #### 【3】行和列 grid-template-columns、 grid-template-rows

例如--实现2行3列：

     .wrapper1 {
        display: grid;
        grid-template-columns: 200px 100px;
        grid-template-rows: 100px 30px 20px;
      }

      <div class="wrapper1">
       <div>1</div>
       <div>2</div>
       <div>3</div>
       <div>4</div>
       <div>5</div>
       <div>6</div>
     </div>



![简单grid网格](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/css_grid_layout/grid_layout.png);

* #### 【4】设置items子元素--定位和调整items子元素的大小；grid-column和grid-row
   * ##### 【网格线划分，而不是网格】

具体实现

    .wrapper2 {
          display: grid;
          grid-template-columns: 100px 100px 100px;
          grid-template-rows: 100px 100px 100px;
        }
    .item1 {
         grid-column: 1/3; // 等同于grid-column-start:1; grid-column-end:3;
         从第一条分割线到第三条分割线，相当于占了2列；
        }
    .item3 {
        grid-row-start: 2;
        grid-row-end: 4;
        }
    .item4 {
        grid-column-start: 2;
        grid-column-end: 4;
        } 

     <div class="wrapper2">
       <div class="item1">1</div>
       <div class="item2">2</div>
       <div class="item3">3</div>
       <div class="item4">4</div>
       <div class="item5">5</div>
       <div class="item6">6</div>
     </div>

![grid_items调整单项](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/css_grid_layout/grid_items.png);

* #### 【5】圣杯布局+自适应布局实现

具体代码如下：

     .container {
         display: grid; 
         grid-template-columns: repeat(12, 1fr); //创建一个12列的布局，每列都是一个特单位宽度(总宽度的1/12)
         grid-template-rows: 50px 300px 50px;
         grid-gap: 5px; // 在网格布局中网格项之间的间隙
         grid-template-areas: // 任意网格区域
               "m m m m m m h h h h h h"
               "c c c c c c c c c c c c"
               "f f f f f f f f f f f f";
     }
     // 利用grid-template-areas,仅更改css即可自适应布局
      @media screen and (min-width: 640px) {
         .container {
            grid-template-areas: 
                  ". h h h h h h h h h h ." 
                  "m m c c c c c c c c c c"
                  "f f f f f f f f f f f f";
             }
         }
     .header {
          background-color: #8c8c8c;
          grid-area: h;
    }
    .menu {
         background-color: #3c3c3c;
         grid-area: m;
    }
    .content {
         background-color: #999999;
        grid-area: c;
    }
    .footer {
       background-color: #8c8c8c;
       grid-area: f;
    }

     <div class="container">
        <div class="header">Header</div>
        <div class="menu">Menu</div>
        <div class="content">Content</div>
        <div class="footer">Footer</div>
     </div>


![圣杯布局+自适应布局实现1](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/css_grid_layout/grid_responsive_1.png)

![圣杯布局+自适应布局实现2](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/css_grid_layout/grid_responsive_2.png)



