---
layout: post
title:  "Angularjs+Bootstrp实现多选按钮"
date:   2017-09-09 09:43:20 +0800
categories: jekyll update
---

## 利用Angularjs实现多选按钮 ---布局使用bootstrap

### 执行效果类似：
![效果图](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/angular_achieve_checkbox/result.png)


### html页面代码
 ![html部分代码](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/angular_achieve_checkbox/html_code.png) 

### js代码

> var vm = $scope.vm = {
 reason: "",
 roleStr=''
 };
>
$scope.choseRole=function(reason){
>
   if(vm.roleStr.toString().indexOf(reason)>-1){
>
  vm.roleStr=vm.roleStr.toString().replace(reason,'');
>    }
>
>else{
>   vm.roleStr=vm.roleStr+reason;
  }
  >
}


### css代码

>.d-selecte-off{
  border: 2px solid #ddd ;
  background-color: #ddd;
}

>.d-selecte-on{
  border: 2px solid #379807 ;
  background-color: white;
}


