---
layout: default
title:  "JsonStr VS JsonObj!"
date:   2017-10-19 14:19:40 +0800
categories: jekyll update
---
## JSON字符串和JSON对象区别：

## 【1】JSON对象
![json对象](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonObj.png)
![json对象打印结果](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonObj_console.png)

var jsonObj = {
 name: '胖海葵',
 age: 10,
 sex: '女'
 };
 console.log(jsonObj);// json对象
 console.log(typeof jsonObj);//Object
 console.log(JSON.stringify(jsonObj));//  {"name": "胖海葵","age": 10,"sex": "女"}


## 【2】JSON字符串
----因为字符串的格式符合json的格式，故叫json字符串

### 书写注意：json字符串key与value必须全部使用双引号，否则转为对象时会报错；
### (Uncaught SyntaxError:Unexpected token 'in JSON at position at JSON.parse()');

![json错误字符串](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonstr1.png)
![json错误字符串打印结果](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonstr1_console.png)

![json正确字符串](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonstr2.png)
![json正确字符串打印结果](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/jsonStr_vs_jsonObj/jsonstr2_console.png)

var jsonStr1 = "{'name':'胖海葵','age':10,'sex':'女'}";
console.log(jsonStr1); //  {"name": "胖海葵","age": 10,"sex": "女"}
console.log(typeof jsonStr1);  //string
console.log(JSON.parse(jsonStr1)); //Uncaught SyntaxError:Unexpected token 'in JSON at position at JSON.parse()'

var jsonStr2 = '{"name": "胖海葵","age": 10,"sex": "女"}';
console.log(jsonStr2);//  {"name": "胖海葵","age": 10,"sex": "女"}
console.log(typeof jsonStr2); //string
console.log(JSON.parse(jsonStr2)); // json对象


## 【3】JSON对象和JSON字符串的转换
### [1]JSON对象转为JSON字符串 ：JSON.stringify(jsonObj);
### [2]JSON字符串转为JSON对象：JSON.parse(jsonStr);