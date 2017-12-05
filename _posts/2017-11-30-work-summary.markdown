---
layout: post
title:  "WEB小知识点汇总"
date:   2017-11-30 09:43:20 +0800
categories: jekyll update
---
本文仅用于记录工作中的小知识点：


## 【20171127-20171201】

### 一、项目相关

* 【1】Ajax+Promise 异步请求--直调后台(go语言)接口

具体代码如下：--需要先导入$q依赖;

     function getDataLIst(params){
        var deferred=$q.defer();
        var promise=deferred.promise;
        $.ajax({
            url:'api/project/sale',
            data:JSON.stringfy({
                cmd:'getList',
                request_id:12345,
                session_key:globalService.getSession();
                body:params
                }),
            contentType:'application/json,charset=utf-8',
            dataType:'json',
            type:'post',
            success:function(data){
                 deferred.resolve(data);},
            erro:function(){
                deferred.reject();}
            });
         return promise;
     }

* 【2】图片标签 
  
图片标签仅仅是img

       <img  src="" />

* 【3】分支代码书写时，尽量不要在分支中return---改为多分支实现；如果一个分支为空，则留一个空行；

### 二、响应式设计

* 【1】允许网页宽度自动调整----加viewport元标签
   
具体代码如下：

     <meta name="viewport" content="width=device-width,initial-scale=1" >

* 【2】设置*{box-sizing:border-box}
     *border和padding值均包含在width中；margin另算；
* 【3】不能使用绝对宽度+使用相对字体大小；
* 【4】滚动布局float,如果宽度不够，后面元素会自动滚动到前面元素下方，不会再水平方向溢出；
* 【5】使用css的@media规则(min-width);
* 【6】图片使用自适应：img{max-width:100%}
* 【7】.flow-opposite,实现其在移动端优先显示，且在大屏幕中右侧显示的列；
* 【8】创建一个容器包含页面上所有标签，并用于控制页面的最大宽度；
* 【9】列包含在行中，在大屏幕中用float:left将列水平排列，然后运用padding设置相邻两列之间的间隙，请忘掉margin；

## 【20171120-20171124】

### 一、CSS相关
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


### 二、项目相关：

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
