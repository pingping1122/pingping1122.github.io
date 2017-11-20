---
layout: post
title:  "Web 基础知识"
date:   2017-11-07 09:43:20 +0800
categories: jekyll update
---
本文参考至：
[前端面试题库](https://www.nowcoder.com/ta/front-end-interview)

##【一】、Cookie VS Web Storage

#### 【1】Cookie的弊端
cookie----持久保存客户端数据，分担了服务器存储的负担，有很多局限；
[1]每个特定的域名下最多存储20个cookie，且cookie的最大大约为4096字节，为了兼容性，一般不能超过4095字节；
     
* 1.IE6或更低版本最多20个cookie
* 2.IE7和之后的版本最后可以有50个cookie。
* 3.Firefox最多50个cookie
* 4.chrome和Safari没有做硬性限制
* 5.IE和Opera 会清理近期最少使用的cookie，Firefox会随机清理cookie

IE 提供了一种存储可以持久化用户数据，叫做uerData，从IE5.0就开始支持。每个数据最多128K，每个域名下最多1M。这个持久化数据放在缓存中，如果缓存没有清理，那么会一直存在.

优点：极高的扩展性和可用性；
* 1.通过良好的编程，控制保存在cookie中的session对象的大小。
* 2.通过加密和安全传输技术（SSL），减少cookie被破解的可能性。
* 3.只在cookie中存放不敏感数据，即使被盗也不会有重大损失。
* 4.控制cookie的生命期，使之不会永远有效。偷盗者很可能拿到一个过期的cookie。

缺点：
* 1.Cookie数量和长度的限制，每个Domain最多只能有20条cookie，每个cookie的长度不能超过4KB,否则会被截掉；
* 2.安全性问题，如果cookie被人拦截了，就可以获取所有的session信息，解释加密页于事无补，因为他们只需要原样转发cookie就可以达到目的；
* 3.有些状态不可能保存在客户端，例如，为了防止重复提交表单，我们需要在服务器端保存一个计数器，如果保存在客户端，起不到作用；

#### 【2】浏览器本地存储是怎样的？
在较高版本的浏览器中，js提供了sessionStorage和globalStorage两种方式，h5中提供了localStorage替代了globalStorage；

html5中的Web Storage包括了两种存储方式：sessionStorage和localStorage。

sessionStorage用于本地存储一个会话(session)中的数据，这些数据只有在一个会话中的页面才能访问并当会话结束后数据也随之销毁。因此sessionStorage不是一种持久会的本地存储，仅仅是会话级别的存储；

而localStorage用于持久化的本地存储，除非主动删除数据，否则数据是永远不会过期的；

#### 【3】Web Storage 与Cookie的区别
Web Storage是为了更大容量设计的。Cookie的大小是受限的，并且每次你请求一个新的页面的时候cookie都会被发送过去，这样无形中浪费了带宽，另外cookie还需要指定作用域，不可以跨域调用；

webstorage拥有setItem removeItem clear等方法，不想cookie需要前端开发者自己封装setCookie和getCookie；

cookie也是不可或缺的--cookie的作用是与服务器进行交互，作为http规范的一部分存在，而webstorage仅仅是为了在本地存储数据而生；

浏览器的支持除了IE７及以下不支持外，其他标准浏览器都完全支持(ie及FF需在web服务器里运行)，值得一提的是IE总是办好事，例如IE7、IE6中的UserData其实就是javascript本地存储的解决方案。通过简单的代码封装可以统一到所有的浏览器都支持web storage。

localStorage和sessionStorage都具有相同的操作方法，例如setItem、getItem和removeItem等

##【二】、CSS

#### 【1】CSS中 link 和@import 的区别是？

* 1.link属于HTML标签，@import是css提供的；
* 2.页面被加载的时候，link会同时被加载，而@import引用的css会等到页面被加载完再加载；
* 3.import只在IE5以上才能被识别，而link是HTML标签，无兼容问题；


#### 【2】position的absolute与fixed共同点与不同点

共同点：
* 1.改变行内元素的呈现方式，display被设为inline-block；
* 2.让元素脱离普通流，不占据空间；
* 3.默认会覆盖到非定位元素上；

不同点：
* absolute的根元素是可以设置的，而fixed的根元素固定为浏览器窗口。当你滚动网页，fixed元素与浏览器窗口之间的距离是不变的；


#### 【3】css的盒子模型
* 盒模型：内容、填充、边界、边框；
* 有两种，IE盒子模型，标准W3C盒子模型；IE的content部分包含了border和padding；

IE8以下浏览器的盒模型中定义的元素的宽高包括内边距和边框;

#### 【4】css选择符
* 可继承的样式：font-size、font-family、color、text-indent；
* 不可继承的样式；border、padding、margin、width、height；
优先级算法：
* 1.优先级就近原则，同权重情况下样式定义最近者为准;
* 2.载入样式以最后载入的定位为准;
* 3.!important >  id > class > tag  
* 4.important 比 内联优先级高，但内联比 id 要高

 inline-block 像行内元素一样显示，但其内容像块类型元素一样显示。

#### 【5】css3有哪些特性？
* 1. CSS3实现圆角（border-radius），阴影（box-shadow），
* 2. 对文字加特效（text-shadow、），线性渐变（gradient），旋转（transform）
* 3. transform:rotate(9deg) scale(0.85,0.90) translate(0px,-30px) skew(-9deg,0deg);// 旋转,缩放,定位,倾斜
* 4. 增加了更多的CSS选择器  多背景 rgba
* 5. 在CSS3中唯一引入的伪类是 ::selection.
* 6. 媒体查询，多栏布局
* 7. border-image

#### 【6】为什么要初始化css样式？
因为浏览器的兼容问题，不同浏览器对有些标签的默认值是不同的，如果没有对css初始化会出现浏览器之间的页面显示差异。当然初始化会对SEO有一定影响；

最简单的初始化方式：（不建议）

     {padding: 0; margin: 0;}

淘宝样式初始化：

    body, h1, h2, h3, h4, h5, h6, hr, p, blockquote, dl, dt, dd, ul, ol, li, pre, form, fieldset, legend, button, input, textarea, th, td { margin:0; padding:0; }
    body, button, input, select, textarea { font:12px/1.5tahoma, arial, \5b8b\4f53; }
    h1, h2, h3, h4, h5, h6{ font-size:100%; }
    address, cite, dfn, em, var { font-style:normal; }
    code, kbd, pre, samp { font-family:couriernew, courier, monospace; }
    small{ font-size:12px; }
    ul, ol { list-style:none; }
    a { text-decoration:none; }
    a:hover { text-decoration:underline; }
    sup { vertical-align:text-top; }
    sub{ vertical-align:text-bottom; }
    legend { color:#000; }
    fieldset, img { border:0; }
    button, input, select, textarea { font-size:100%; }
    table { border-collapse:collapse; border-spacing:0; }  


#### 【7】解释下 CSS sprites，以及你要如何在页面或网站中使用它
CSS Sprites 其实就是把网页中一些背景图片整合到一张图片文件中，再利用 CSS 的"background-image"，"background-repeat"，"background-position" 的组合进行背景定位，background-position 可以用数字能精确的定位出背景图片的位置。这样可以减少很多图片请求的开销，因为请求耗时比较长；请求虽然可以并发，但是也有限制，一般浏览器都是6个。对于未来而言，就不需要这样做了，因为有了 http2。

#### 【8】iframe的优缺点：
优点：
1. 解决加载缓慢的第三方内容如图标和广告等的加载问题
2. Security sandbox
3. 并行加载脚本

缺点：
1. iframe会阻塞主页面的Onload事件
2. 即时内容为空，加载也需要时间
3. 没有语意


## 【三】、HTML
#### 【1】HTML与XHTML——二者有什么区别
最主要的不同：
XHTML 元素必须被正确地嵌套。
XHTML 元素必须被关闭。
标签名必须用小写字母。
XHTML 文档必须拥有根元素。


## 【四】、web

#### 【1】如何实现浏览器内多个标签页之间的通信
调用localStorage 或cookie；

#### 【2】webSocket如何兼容低浏览器？
Adobe Flash Socket 、 ActiveX HTMLFile (IE) 、 基于 multipart 编码发送 XHR 、 基于长轮询的 XHR

#### 【3】如何对网站的文件和资源进行优化？
* 1.文件合并；
* 2.文件最小化、文件压缩
* 3.使用CDN托管；
* 4.缓存的使用（多个域名来提供缓存）

#### 【4】减少页面加载时间的方法：
* 1. 优化图片 
* 2. 图像格式的选择（GIF：提供的颜色较少，可用在一些对颜色要求不高的地方） 
* 3. 优化CSS（压缩合并css，如 margin-top, margin-left...) 
* 4. 网址后加斜杠（如www.campr.com/目录，会判断这个目录是什么文件类型，或者是目录。） 
* 5. 标明高度和宽度（如果浏览器没有找到这两个参数，它需要一边下载图片一边计算大小，如果图片很多，浏览器需要不断地调整页面。这不但影响速度，也影响浏览体验。 
当浏览器知道了高度和宽度参数后，即使图片暂时无法显示，页面上也会腾出图片的空位，然后继续加载后面的内容。从而加载时间快了，浏览体验也更好了） 
* 6. 减少http请求（合并文件，合并图片）

#### 【5】使用那些工具来测试代码的性能？

1. Profiler
2. JSPerf（http://jsperf.com/nexttick-vs-setzerotimeout-vs-settimeout）
3. Dromaeo

#### 【6】FOUC 如何避免？
FOUC - Flash Of Unstyled Content 文档样式闪烁
<style type="text/css" media="all">@import "../fouc.css";</style> 
而引用CSS文件的@import就是造成这个问题的罪魁祸首。IE会先加载整个HTML文档的DOM，然后再去导入外部的CSS文件，因此，在页面DOM加载完成到CSS导入完成中间会有一段时间页面上的内容是没有样式的，这段时间的长短跟网速，电脑速度都有关系。
解决方法简单的出奇，只要在<head>之间加入一个<link>或者<script>元素就可以了。

#### 【7】JSON--JSON(JavaScript Object Notation) 是一种轻量级的数据交换格式。它是基于JavaScript的一个子集。数据格式简单, 易于读写, 占用带宽小。

#### 【8】
document.write 只能重绘整个页面

innerHTML 可以重绘页面的一部分

#### 【9】性能优化方法
* 1. 减少http请求次数：CSS Sprites, JS、CSS 源码压缩、图片大小控制合适；网页 Gzip，CDN 托管，data 缓存 ，图片服务器
* 2. 前端模板 JS + 数据，减少由于HTML标签导致的带宽浪费，前端用变量保存 AJAX 请求结果，每次操作本地变量，不用请求，减少请求次数
* 3. 用 innerHTML 代替 DOM 操作，减少 DOM 操作次数，优化 javascript 性能
* 4. 当需要设置的样式很多时设置 className 而不是直接操作 style
* 5. 少用全局变量、缓存DOM节点查找的结果。减少 IO 读取操作
* 6. 避免使用 CSS Expression（css表达式)又称 Dynamic properties(动态属性)
* 7. 图片预加载，将样式表放在顶部，将脚本放在底部，加上时间戳

#### 【10】前端的安全问题
* 1. XSS
* 2. sql注入
* 3. CSRF：是跨站请求伪造，很明显根据刚刚的解释，他的核心也就是请求伪造，通过伪造身份提交POST和GET请求来进行跨域的攻击

完成CSRF需要两个步骤：
* 1. 登陆受信任的网站A，在本地生成 COOKIE
* 2. 在不登出A的情况下，或者本地 COOKIE 没有过期的情况下，访问危险网站B

#### 【11】Flash、Ajax各自的优缺点，在使用中如何取舍？
Flash：
1. Flash适合处理多媒体、矢量图形、访问机器
2. 对CSS、处理文本上不足，不容易被搜索

Ajax：
1. Ajax对CSS、文本支持很好，支持搜索
2. 多媒体、矢量图形、机器访问不足

共同点：
1. 与服务器的无刷新传递消息
2. 可以检测用户离线和在线状态
2. 操作DOM
