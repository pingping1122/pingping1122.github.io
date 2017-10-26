---
layout: post
title:  "html通过js强制下载mp4文件(download)"
date:   2017-10-26 09:43:20 +0800
categories: jekyll update
---
本文参考至：
[Mp4 Download causes browser to play file instead of download](https://stackoverflow.com/questions/21091766/mp4-download-causes-browser-to-play-file-instead-of-download)

## 【H5-download】
#### HTML5的download属性用来强制浏览器下载对应文件，而非打开。

#### Chrome和Firefox等浏览器太过于强大，也许为了增强用户体验，当用户点击的资源文件可以被它们识别的时候（例如pdf会直接在浏览器打开，MP3、 MP4等媒体直接用浏览器内置播放器播放）。

#### 但有时候用户希望直接下载而不是在浏览器上看看,如果你的站点是有服务器端的，你可以通过配置.htaccess文件来使得那些文件可以被下载。如果你的站点是被WordPress.com或者github页面托管的（静态页面），那么请考虑使用\<a>标签的download属性,属性值会对下载的文件重命名;

     <a href="downloadpdf.php" download="download.pdf">

#### 如果你确定这个资源是用户肯定会下载的，就可以加上这个属性，还可以用 JS 或者手动改变想要保存的文件名。在html里创建一个是下载链接是方便的，添加一个\<a>标签和指向文件的href属性就行了。

## 【注意】：
#### Firefox考虑到安全问题，该下载文件必须是从自己的服务器或域名中的，否则将在浏览器中打开。在Chrome和Opear中，如果说下载文件不是在子集的服务器或域名中，这些浏览器会忽视download属性，换句话来说，文件名不变。

## 【火狐等浏览器打开地址而非下载--解决方案】

### html:
     <a href="http://yoursite.com/file?id=1234">Download Hello.mp4</a>

### php:
      header('Content-Disposition: attachment; filename="'.$nameOfFile.'"');
      header('Content-Type: application/force-download');
