---
layout: post
title:  Angularjs实现多选按钮
date:   2017-09-09 16:01:20 +0800
categories: jekyll update
---
## 利用Angularjs实现多选按钮 ---布局使用bootstrap

### html页面代码
<div>
<button class= "btn btn-default est-lab" ng-class="{true: 'selecte-on', false: 'selecte-off'}[vm.reasonStr.indexOf('a') > -1]" ng-click="choseReason('a');">生产商</button>
<button class= "btn btn-default est-lab" ng-class="{true: 'selecte-on', false: 'selecte-off'}[vm.reasonStr.indexOf('b') > -1]" ng-click="choseReason('b');">销售商</button>
<button class= "btn btn-default est-lab" ng-class="{true: 'selecte-on', false: 'selecte-off'}[vm.reasonStr.indexOf('c') > -1]" ng-click="choseReason('c');">芯片商</button>
<button class= "btn btn-default est-lab" ng-class="{true: 'selecte-on', false: 'selecte-off'}[vm.reasonStr.indexOf('d') > -1]" ng-click="choseReason('d');">品牌商</button>


<button class="btn btn-default est-lab"
          ng-class="{true: 'd-selecte-on', false: 'd-selecte-off'}
          [vm.roleStr.indexOf('1') > -1]"
          ng-click="choseRole('1');">芯片商
</button>
<button class="btn btn-default est-lab"
        ng-class="{true: 'd-selecte-on', false: 'd-selecte-off'}
        [vm.roleStr.indexOf('2') > -1]"
        ng-click="choseRole('2');">方案商
</button>
<button class="btn btn-default est-lab"
        ng-class="{true: 'd-selecte-on', false: 'd-selecte-off'}
        [vm.roleStr.indexOf('3') > -1]"
        ng-click="choseRole('3');">生产商
</button>
<button class="btn btn-default est-lab"
        ng-class="{true: 'd-selecte-on', false: 'd-selecte-off'}
        [vm.roleStr.indexOf('4') > -1]"
        ng-click="choseRole('4');">品牌商
</button>
</div>

### js代码

 var vm = $scope.vm = {
 reason: "",
        roleStr: ''
      };
      $scope.choseRole = function (reason) {
        if (vm.roleStr.toString().indexOf(reason) > -1) {
          vm.roleStr = vm.roleStr.toString().replace(reason, "");
        }
        else {
           if(vm.roleStr.length < 2){
            vm.roleStr = vm.roleStr + reason;}
            else{
                alert("最多只能选中2个标签");
            }
        }
      };


### css代码

.d-selecte-off{
  border: 2px solid #ddd ;
  background-color: #ddd;
}
.d-selecte-on{
  border: 2px solid #379807 ;
  background-color: white;
}

###执行效果如图：----图标自己酌情加

