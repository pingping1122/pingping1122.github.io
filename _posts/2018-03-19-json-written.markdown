---
layout: post
title:  "JSON书写规范+VS--JS对象"
date:   2018-03-18 09:20:20 +0800
categories: jekyll update
---

### 一、JSON书写规范
* json对象中不包含注释；
* 使用双引号
* 扁平化数据或结构化数据；

扁平化：
    
     {
        "company":"google",
        "addressline":"12121th",
        "addressline2":"4th"
     }

结构化---更有意义，但注意不能为了方便而将数据任意分组
    
     {
        "company":"google",
        "address":{
            "line":"12121th",
             "line2":"4th",
            }
     }

* 属性名
   * 具有意义的名称
   * 属性名为驼峰式的
   * 首字母必须为字母、下划线或美元符号，随后可有数字
   * 数组类型属性名应为复数，其他应为单数；
* 属性值
   * --不能为函数、undefined、NaN；
   * 空或null的属性值--考虑从json中去掉，除非有强存在意义；

### 二、JSON对象+JS对象

JSON对象|JS对象
:--- | :---
仅是一种数据格式 | 对象的实例
可以跨平台数据传输 | 不能传输
键值对、键必须加双引号、值不能为函数、undefined和null | 键值对、值可以为任何值
json->js JSON.parse() | js->json JSON.stringfy()

