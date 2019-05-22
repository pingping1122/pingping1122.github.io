---
layout: post
title:  "利用vue-cli脚手架搭建spa种子应用+vue的调用顺序"
date:   2019-05-22 09:47:03 +0800
categories: jekyll update
---

## 一、第一次使用Vue-cli搭建SPA应用

![spa效果图](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/vue/result.gif)


#### (1)安装node、npm、cnpm并查看版本号

     node -v  // 查看node版本号
     npm -v   // 查看npm版本号
     cnpm -v  // 查看cnpm版本号

#### (2)全局安装vue-cli

    cnpm install -g vue-cli  // 全局安装

    vue -V(大写)    //查看是否安装成功

#### (3)进入项目所在文件夹--生成项目

    vue init webpack  vue-cli-spa-seed(项目名字)   // 生成项目
    Project name: test // 项目名字
    Project description: A vue.js project // 项目描述
    Author :xxx // 作者
    Vue build:standalone //打包方式
    Use ESLint to lint your code  //  ****一定是N,不使用ESLint代码规范 ***
    xxxx：n    // 单元测试

#### (4)进入项目

    cnpm install  // 安装项目依赖

#### (5) 启动项目

     cnpm run dev

![搭建的目录结构](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/vue/vue-cli-structure.png)

#### (6)添加About路由

##### 1、在components文件夹下添加About.vue文件

##### 2、在app.vue中router组件前添加  

     <router-link v-bind:to="'/'">Home</router-link>    
     <router-link v-bind:to="'/About'">About</router-link>  
     <router-view/>

##### 3、在router/index.js中添加

     import About from '@/components/About'
     Vue.use(Router);
      export default new Router({
        routes: [
          {
            path: '/',
            name: 'HelloWorld',
            component: HelloWorld
          },
          {
            path: '/About',
            name: 'About',
            component: About
         }
       ]
     })

#### (7)打包上线

     cnpm run build

打包完成后，会生成dist文件夹。项目上线时，只需将dist文件夹放到服务器就ok啦。



## 二、Vue加载过程（index.html、src/main.js、 src/App.vue、 src/router/index.js）

![加载顺序](https://raw.githubusercontent.com/pingping1122/pingping1122.github.io/master/images/vue/vue-cli-spa.png)

#### （1）index.html中建立一个id为app的div

    <body>
        <div id="app"></div>
    </body>

#### (2)在main.js中新建一个实例。main.js和App.vue同级，在main.js中引入App.vue

     import App from './App'
     new Vue({
      el: '#app',   // el决定对象装在位置--index.html中DOM元素#app
      router,       // 路由
      components: { App },  // App组件
      template: '<App/>'     // 使用的模板
    });

* index.html中#app指定绑定的目标，vue中#app提供填充内容，两者运行时指的是同一个DOM元素。
* app.vue是主组件，所有页面都是在App.vue下进行切换的，所有的路由也是其子组件。
* router.js中配置的路由信息会渲染到App.vue中的 router-view组件中  

#### (3)App.vue组件渲染main.js,main.js挂载在index.html中；

     <template>   // 此处注意template下只能有一个父标签
       <div id="app">
      <router-view/>
      </div>
    </template>
