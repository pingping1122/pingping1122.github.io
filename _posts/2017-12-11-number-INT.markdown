---
layout: post
title:  "JS中数字取整"
date:   2017-12-11 09:20:20 +0800
categories: jekyll update
---

JS中数字取整：

#### 一、【标准取整】

* **parseInt(str)**
  * parseInt('2016nov'); // 2016
  * parseInt('weyu'); // NAN
* **Math.trunc()**--会将数字的小树部分去掉，只保留证书部分；
  * Math.trunc('12.33');//12
  * Math.trunc('dfd');//NAN
* **\~\~Number（双按位非）**
  * console.log(\~\~47.11); // 47
  * console.log(\~\~[]); // 0
* **number\|0(按位或)**
  * console.log(20.15\|0);//20
* **number^0(按位异或)**
  * console.log(20.12^0);//20

#### 二、【舍入舍去取整】
* **Math.round()--四舍五入** 
* **Math.floor()--向下取整(<=)**
* **Math.ceil()--向上取整(>=)**

