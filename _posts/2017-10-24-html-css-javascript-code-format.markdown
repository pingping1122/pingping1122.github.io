---
layout: post
title:  "html+css+javascript 书写规范"
date:   2017-10-24 09:43:20 +0800
categories: jekyll update
---
## 【HTML规范】：

-----------------------------------------

### 【一】、代码规范：
#### [1]DOCTYPE声明
---HTML文件必须加上DOCTYPE声明，并统一使用HTML5的文档声明；

    <!DOCTYPE html> 

#### [2]页面语言LANG
---zh-CN(中国大陆)--浏览器和操作系统的兼容性较好；

    <html lang="zh-CN">

#### [3]CHARSET
---HTML5中默认的字符编码是UTF-8,请尽量统一写成标准的'UTF-8',而不要写成'utf-8'或'utf8'或'UTF8';

    <meta charset="UTF-8">

#### [4]元素及标签闭合
---所有的开始标签和结束标签的元素都要写上起止标签，某些允许省略开始标签和结束标签的元素亦要写上；

---空元素标签都不加'/'字符

推荐写法：

    <div>
    <h1>我是h1标签</h1>
    <p>我是一段文字，有始有终，浏览器能正确解析</p>
    </div>
    <br>

#### [5]书写风格
---(1)HTML代码大小写---HTML标签名、类名、标签属性和大部分属性值统一用小写；

---(2)类型属性---不需要为CSS、JSz制定类型属性，HTML5中默认已包含；

推荐：

    <link rel="stylesheet" href="">
    <script src=""></script>

---(3)元素属性---元素属性值使用双引号语法，且属性值可以写上的都写上；

推荐：

    <input type="text">
    <input type="radio" name="name" checked="checked">

不推荐：

    <input type='text'>
    <input type='radio' name="name" checked>

---(3) 特殊字符引用---在html中不能使用小于号和大于号特殊字符，浏览器会将它们作为标签解析，若要正确显示，在html源代码中要使用字符实体；

---(4)代码缩进---统一使用四个空格进行代码缩进，使得各编辑器表现一致(各编辑器有相关配置)；

---(5)纯数字输入

     推荐使用：<input type="tel">   tel---定义用于电话号码的数字字段

     不推荐使用：<input type="number">  number---定义带有spinner空间的数字字段

---(6)代码嵌套--每个块状元素独立一行，内联元素可选；段落元素与标题元素只能嵌套内联元素；

### 【二】、注释规范

#### [1]单行注释
--- 一般用于简单的描述，如某些状态描述，属性描述等；
--- 注释内容前后各一个空格字符，注释位于要注释代码的上面，单独占一行；

#### [2]多行注释
--- 一般用于描述模块的名称一级模块开始与结束的位置；

--- 注释内容前后各一个空格字符;

--- 模块与模块之间相隔一行；

     <!-- S Comment Text --> 表示模块开始，
     <!-- E Comment Text --> 表示模块结束，



#### [3]嵌套模块注释

推荐使用：

    <!-- S Comment Text A -->
    <div class="mod_a">
    <div class="mod_b">
       ...
    </div>
    <!-- /mod_b -->
    <div class="mod_c">
        ...
    </div>
    <!-- /mod_c -->
     </div>
     <!-- E Comment Text A -->

### 【二】、文件规范

#### [1] HTML5标准模板

    <!DOCTYPE html>
    <html lang="zh-CN">
        <head>
             <meta charset="UTF-8">
             <title>HTML5标准模版</title>
        </head>
        <body>
        </body>
    </html>

#### [2]移动端模板

     <!DOCTYPE html>
    <html lang="zh-CN">
        <head>
           <meta charset="UTF-8">
           <meta name="viewport" content="width=device-width, initial-scale=1.0,  maximum-scale=1.0, user-scalable=no, shrink-to-fit=no" >
           <meta name="format-detection" content="telephone=no" >
           <title>移动端HTML模版</title>
           <!-- S DNS预解析 -->
           <link rel="dns-prefetch" href="">
           <!-- E DNS预解析 --> 
           <!-- S 线上样式页面片，开发请直接取消注释引用 -->
           <!-- #include virtual="" -->
           <!-- E 线上样式页面片 -->
           <!-- S 本地调试，根据开发模式选择调试方式，请开发删除 --> 
           <link rel="stylesheet" href="css/index.css" >
           <!-- /本地调试方式 -->
           <link rel="stylesheet" href="http://srcPath/index.css" >
           <!-- /开发机调试方式 -->
           <!-- E 本地调试 -->
        </head>
        <body>
        </body>
    </html>

### 【三】、webApp--meta

    <meta name="viewport" content="width=device-width, initial-scale=1.0,
     maximum-scale=1.0, user-scalable=no">

* width – viewport的宽度  
* height – viewport的高度  
* initial-scale – 初始的缩放比例  
* minimum-scale – 允许用户缩放到的最小比例 
* maximum-scale – 允许用户缩放到的最大比例 
* user-scalable – 是否允许用户缩放 

## 【图片规范】

-----------------------------------------

#### [1]图片大小

---PC平台单张的图片的大小不应大于 200KB；

---移动平台单张的图片的大小不应大于 100KB；

### [2]图片质量

--- 上线的图片都应该经过压缩处理，压缩后的图片不应该出现肉眼可感知的失真区域
60质量的JPEG格式图片与质量大于60的相比，肉眼已看不出明显的区别，因此保存 JPEG 图的时候，质量一般控制在60，若保真度要求高的图片可适量提高到 80，图片大小控制在 200KB 以内；

### [3]图片引入--CSS Sprites VS Data URI(base64编码)
---HTML 中图片引入不需添加 width、height 属性，alt 属性应该写上：

    <img src="" alt="" >

--- CSS 中图片引入不需要引号

     .jdc {
    background-image: url(icon.png);
    }


## 【CSS规范】

-----------------------------------------

### 【一】、编码规范

#### [1] 样式表编码
---样式文件必须写上@charset规则，并且一定要写在样式文件的第一行首个字符位置开始写，编码名用"UTF-8";
---字符@charset都使用小写字母，不能出现转义符，编码名允许大小写；
---.考虑到在使用"UTF-8"编码情况下BOM对代码的污染和编码显示的问题，在可控范围下，坚决不使用BOM;

### 【二】、代码风格
#### [1]书写尽量使用展开格式：

     .jdc{
    display: block;
    width: 50px;
    }

#### [2]代码大小写
样式选择器，属性名，属性值关键字全部使用小写字母书写，属性字符串允许使用大小写；

#### [3]选择器
* 尽量少用通用选择器* 
* 不使用ID选择器
* 不使用无具体语义定义的标签选择器

#### [4]代码缩进
----统一使用四个空格进行代码缩进，使得各编辑器表现一致(各编辑器有相关配置)；

#### [5]分号
--- 每个属性声明末尾都要加分号；

#### [6]代码易读性
---左括号与类名之间一个空格，冒号与属性值之间一个空格；
---逗号分隔的取值，逗号之后一个空格；
---为单个css选择器开启新行；

     .jdc, 
     .jdc_hd {
       color: #ff0; 
       }

---不要为0指明单位；
---css属性值需要用到引号时，统一使用单引号

     .jdc { 
    font-family: 'Hiragino Sans GB';
    }

### 【三】、属性书写顺序
* 布局定位属性：display / position / float / clear / visibility / overflow
* 自身属性：width / height / margin / padding / border / background
* 文本属性：color / font / text-decoration / text-align / vertical-align / white- space / break-word
* 其他属性（CSS3）：content / cursor / border-radius / box-shadow / text-shadow / background:linear-gradient

### 【四】、CSS3浏览器私有前缀写法

     .jdc {
    -webkit-border-radius: 10px;
    -moz-border-radius: 10px;
    -o-border-radius: 10px;
    -ms-border-radius: 10px;
    border-radius: 10px;
    }      

### 【五】、注释规范
#### [1]单行注释---注释内容第一个字符和最后一个字符都是一个空格字符，单独占一行，行与行之间相隔一行；
 
     /* Comment Text */
     .jdc{}

#### [2] 模块注释---注释内容第一个字符和最后一个字符都是一个空格字符，
\/* 与模块信息描述占一行，多个横线分割符-与*/ 占一行，行与行之间相隔两行；

     /* Module A
     ---------------------------------------------------------------- */
     .mod_a {}

#### [3]文件信息注释---在样式文件编码声明@charset语句下面注明页面名称、作者、创建日期等信息；

    @charset "UTF-8";
    /**
    * @desc File Info
    * @author Author Name
    * @date 2015-10-10
     */ 

### 【六】、媒体查询
#### [1]判断设备横竖屏

     /* 横屏 */
    @media all and (orientation :landscape) {
     }
     /* 竖屏 */
    @media all and (orientation :portrait) {
        }

#### [2]判断设备宽高

     /* 设备宽度大于 320px 小于 640px-all 所有设备 */
     @media all and (min-width:320px) and (max-width:640px) {
     }


     // screen 显示器类
    @media screen and (min-width: 1200px) {
        css-code;
    }
    @media screen and(min-width: 960px) and (max-width: 1199px) {
        css-code;
    }
    @media screen and(min-width: 768px) and (max-width: 959px) {
        css-code;
    }
    @media screen and(min-width: 480px) and (max-width: 767px) {
        css-code;
    }
    @media screen and (max-width: 479px) {
        css-code;
    }

#### [3]判断设备像素比

       /* 设备像素比为 1 */
    @media only screen and (-webkit-min-device-pixel-ratio: 1), only screen and (min-device-pixel-ratio: 1) {
    }
    /* 设备像素比为 1.5 */
    @media only screen and (-webkit-min-device-pixel-ratio: 1.5), only screen and (min-device-pixel-ratio: 1.5) { 
    }
    /* 设备像素比为 2 */
    @media only screen and (-webkit-min-device-pixel-ratio: 2), only screen and (min-device-pixel-ratio: 2) { 
    }  

## 【命名规范】

-----------------------------------------

### 【一】、HTML/CSS文件命名
---确保文件命名总是以字母开头而不是数字，且字母一律小写，以下划线连接且不带其他标点符号；

### 【二】、ClassName命名
---className的命名应该尽量简短、明确、必须以字母开头命名，且全部字母为小写，单词之间统一使用下划线'_'连接；

#### [1]命名原则：

---祖先模块不能出现下划线，除了是全站公用模块，如mod_系列的命名；

---在子孙模块数量可预测的情况下，严格继承祖先模块的命名前缀；

---在子孙模块超过4级或以上的时候，可以考虑在祖先模块内具有辨识性的独立缩写作为新的子孙模块；


## 【JS规范】

-----------------------------------------

### 【一】、语言规范

### 【二】、代码规范

#### [1]单行代码块
---在单行代码块中使用空格；

     function foo () { return true }
     if (foo) { bar = 0 }

#### [2]大括号风格

    if (foo) {
      bar()
     } else {
     baz()
    }

#### [3]变量命名
 ---统一使用驼峰式命名；

#### [4]拖尾逗号
 ---约束在最后一个元素或属性与闭括号]或}在不同行时可以使用拖尾逗号，当在同一行时，禁止使用拖尾逗号；

#### [5]逗号空格
 ---逗号前后的空格可以提升代码的可读性，约定在逗号后面使用空格，逗号前面不加空格；

#### [6]逗号风格
 ---b标准风格，逗号放置在当前行的末尾；

####  [7]计算属性的空格
 ---约定在对象的计算属性内，禁止使用空格；

    obj['foo']

#### [8]函数调用
---函数调用的时，禁止使用空格；

#### [9]对象字面量的键值缩进
----对象字面量的键和值之间不能存在空格，且要求对象字面量的冒号和值之间存在一个空格；

#### [10]构造函数首字母大写

#### [11]构造函数的参数
---通过new调用构造函数时，约定使用圆括号；

#### [12]变量声明
---约定之声明变量时，一个声明只能有一个变量；

#### [13]操作符的空格
--- 约定操作符前后都需要添加空格；



 
 











