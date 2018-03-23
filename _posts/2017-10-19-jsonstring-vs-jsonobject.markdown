---
layout: default
title:  "JsonStr VS JsonObj!"
date:   2017-10-19 14:19:40 +0800
categories: jekyll update
---
## JSON字符串和JSON对象区别：

## 【1】JSON对象

### json对象
![json对象](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonObj.png)

### json对象打印结果
![json对象打印结果](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonObj_console.png)


## 【2】JSON字符串
----因为字符串的格式符合json的格式，故叫json字符串

## 书写注意：json字符串key与value必须全部使用双引号，否则转为对象时会报错；
### (Uncaught SyntaxError:Unexpected token 'in JSON at position at JSON.parse()');

### json错误字符串
![json错误字符串](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonstr1.png)

### json错误字符串打印结果
![json错误字符串打印结果](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonstr1_console.png)

### json正确字符串
![json正确字符串](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonstr2.png)

### json正确字符串打印结果
![json正确字符串打印结果](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonstr2_console.png)

## 【3】JSON对象和JSON字符串的转换
### [1]JSON对象转为JSON字符串 ：JSON.stringify(jsonObj);
### [2]JSON字符串转为JSON对象：JSON.parse(jsonStr);

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
