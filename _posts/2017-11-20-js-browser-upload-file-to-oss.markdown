---
layout: post
title:  "js 浏览器直传本地文件到OSS"
date:   2017-11-20 09:43:20 +0800
categories: jekyll update
---
本文参考至：
【1】[阿里云-Javascript-SDK-浏览器直传](https://help.aliyun.com/document_detail/32069.html?spm=5176.doc32077.6.739.wkOiRU)
和【2】[阿里云-分片上传-progress进度条](https://help.aliyun.com/document_detail/32072.html?spm=5176.doc32069.6.742.DWPA1f)

工作流程如下：

【1】包含sdk--在html文件的<head>中包含以下标签：

       <script src="http://gosspublic.alicdn.com/aliyun-oss-sdk-4.4.4.min.js"></script>

OSS JavaScript SDK同时支持同步和异步的使用方式：

同步方式：类似协程的方式，基于Generator Function，使用new OSS()创建client,使用co和yield;

异步方式：类似callback的方式，使用new OSS.Wrapper()创建client,API接口返回Promise，使用.then()处理返回结果，使用.catch()处理错误。

这里使用异步：通过new OSS.Wrapper()来创建client，OSS.Wrapper提供了异步接口，类似于callback的方式，在.then()中处理返回的结果，在.catch()中处理错误；

【2】上传文件---下载文件---查看文件列表

>注意：浏览器是不受信任的环境，如果把AccessKeyId和AccessKeySecret直接保存在
>浏览器端，存在极高的风险。建议只在测试时使用明文设置，业务应用中请使用
>STS鉴权模式 和 自签名模式 ,详细说明请参考访问控制、移动端直传。

【上传文件--进度条显示上传进度progress+强制下载而非打开headers配置】

js:

    var progress = function (p) {
      return function (done) {
        var bar = document.getElementById('progress-bar');
        bar.style.width = Math.floor(p * 100) + '%';
        bar.innerHTML = Math.floor(p * 100) + '%';
        done();
      }
    };


    uploadFile = function (file) {   
     service.getToken(params).then(function (data) {
          var storeAs = data.upload_path;
          var client = new OSS.Wrapper({
            accessKeyId: data.body.access_key_id,
            accessKeySecret: data.body.access_key_secret,
            stsToken: data.body.security_token,
            endpoint: data.body.end_point,
            bucket: data.body.bucket_name
          });
          client.multipartUpload(storeAs, file.files[0], {
            headers: {
              'Content-Type': 'application/force-download',
              'Content-Disposition': 'attachment; filename=' + data.upload_path
            },
            progress: progress
          }).then(function (result) {
            console.log('文件上传oss成功！');
          }).catch(function (err) {
            console.log(err);
          });
        });
    }

html:

    <div class="progress ">
          <div id="progress-bar"
               class="progress-bar"
               role="progressbar"
               aria-valuenow="0"
               aria-valuemin="0"
               aria-valuemax="100" style="min-width: 2em;">
            0%
          </div>
        </div>