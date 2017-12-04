---
layout: post
title:  "WEB小知识点汇总"
date:   2017-11-30 09:43:20 +0800
categories: jekyll update
---
本文仅用于记录工作中的小知识点：


## 【20171127-20171201】

## 【20171120-20171124】

### CSS相关
* 【1】flex布局，
   *  若父子布局均为flex，则同一方向上的布局继承至父布局；eg.flex-direction;
   *  设置为flex布局后，其子元素的float、clear、vertical-align失效；
* 【2】水平居中：margin:0 auto;
* 【3】文字垂直居中：让line-height==[父标签].height;
* 【4】css如何实现子元素继承父类的宽高：父元素设置具体宽高+子元素设置100%占比；
* 【5】页面滚动轴实现：overflow；
* 【6】视图相对单位[vh-相对视图高度，vw-相对视图宽度]min-height="100vh";min-width="100vw";
* 【7】absolute元素全页面(窗口)居中

     {
         position:absolute;
         left:0;right:0;top:0;bottom:0;
         margin:auto;
     }
* 【8】子video-100%占比父div，如何实现孙div在子video正中间重叠显示
![需求图](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/work_web_summary/孙div在子Video正中显示.png)

实现方式：

    <div class="father">
     <div class="son"></div>
     <div class="sun"></div>
    </div>

.sun{
    z-index:1000;
    position:absolute;
    top:10rem;
}

* 【9】top与margin区别
   * top/left/right/bottom -是针对absolute布局独有的；margin系列是针对relative；
   * top的绝对定位是相对body或布局为relative的父级元素的绝对定位；而margin是值相对相邻元素的定位；

![top与margin区别](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/work_web_summary/top-vs-margin.png)

* 【10】css可改变鼠标样式；
* 【11】a链接去掉下划线：style="text-decoration:none;"
* 【12】iframe即内联框架，--通过其可实现在网页中插入网页；
* 【13】span之间有空格的实现方式：
    
--在span中间加回车换行符即可实现

      <span>sss</span>
      <span>ddd</span>

【14】三个并列div，2突然变为float，则2跳出文件流，3跑到1下边，如何实现三个仍旧竖着并列；
-----在2的外再套一层，让2的float只影响其父元素，不影响祖先元素的并列；

![不清除浮动情况下，保持正常文件流](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/work_web_summary/不清除浮动情况下，保持正常文件流.png)


###　项目相关：

* 【1】跨域请求 xhrFields:{withCredentials:true;}
* 【2】文件MD5生成插件：【browser-md5-file】     [spark-md5---生成的MD5不正确]
   browser-md5-file使用方式：

html:

    <script src="browser-md5-file.js"></script>
         <button id="upload"></button>

js:

    var el=document.getElementById('upload');
        el.addEventListener('change', handle, false);
        function handle(e){
    var file=e.target.files[0];
    browserMD5File(file,function(err,md5){
     console.log(md5);
    })
    }

* 【3】html中文乱码问题，在html的最前边加编码设置：

html中设置：

    <html>
      <meta charset="utf-8">
    </html>

* 【4】JSON对象名称必须使用双引号""包含起来；
* 【5】生成二维码的插件【QRCode.js】

使用方式：

    html:
    <script src="qrcode.js">
    <div id="qrqr"></div>
    </script>

    js:
    var q=new QRCode('qrqr',{
        // 可设置参数
      width: 256,
      height: 256,
      colorDark : '#000000', // 前景色
      colorLight : '#ffffff',// 背景色
      correctLevel : QRCode.CorrectLevel.H // 容错级别
    });
    q.clear();
    q.makeCode('二维码内容');
