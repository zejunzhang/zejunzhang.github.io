title: "vue简明教程"
date: 2017-04-03 10:00:00 +0800
update: 2017-04-03 10:00:00 +0800
author: zhengwei
cover: "-/images/vue.jpg"
tags:
    - 前端框架
preview: 优雅、简洁的前端框架

---

<!-- TOC -->

- [学习目标](#学习目标)
- [学习建议](#学习建议)
- [相关代码下载地址](#相关代码下载地址)
- [问题反馈](#问题反馈)
- [从angular 1.x中学到的概念review](#从angular-1x中学到的概念review)
    - [框架与库的区别](#框架与库的区别)
    - [SPA与多页面的区别](#spa与多页面的区别)
    - [mvc,mvvm](#mvcmvvm)
    - [mvc和mvvm的作用：](#mvc和mvvm的作用)
    - [如何安装angular.js](#如何安装angularjs)
    - [数据绑定之单向数据绑定](#数据绑定之单向数据绑定)
    - [双向数据绑定](#双向数据绑定)
    - [$watch](#watch)
    - [filter过滤器](#filter过滤器)
    - [指令](#指令)
    - [自定义指令](#自定义指令)
        - [示例](#示例)
        - [常见属性](#常见属性)
    - [ngRoute路由](#ngroute路由)
    - [todoMVC的实现思路](#todomvc的实现思路)
- [vue基础知识](#vue基础知识)
    - [说明](#说明)
    - [谁在用](#谁在用)
    - [安装](#安装)
    - [chrome相关插件](#chrome相关插件)
        - [使用注意](#使用注意)
    - [visual studio code编辑器相关插件](#visual-studio-code编辑器相关插件)
    - [vue的特点](#vue的特点)
    - [hello world](#hello-world)
        - [示例](#示例-1)
    - [讲解](#讲解)
        - [注意事项](#注意事项)
    - [单次绑定](#单次绑定)
    - [实现值加1](#实现值加1)
    - [实现值加1升级版](#实现值加1升级版)
    - [为什么vue的性能这么高？](#为什么vue的性能这么高)
    - [双向数据绑定的原理](#双向数据绑定的原理)
    - [表单控件](#表单控件)
    - [v-bind指令](#v-bind指令)
    - [watch监视](#watch监视)
    - [计算属性](#计算属性)
        - [用计算属性替代监视](#用计算属性替代监视)
        - [用计算属性替代filter](#用计算属性替代filter)
    - [v-bind:class](#v-bindclass)
    - [v-if,v-else](#v-ifv-else)
    - [v-show](#v-show)
    - [v-for](#v-for)
    - [v-cloak](#v-cloak)
    - [事件处理器 v-on](#事件处理器-v-on)
    - [事件对象event](#事件对象event)
    - [修饰符](#修饰符)
    - [组件](#组件)
        - [组件使用注意事项](#组件使用注意事项)
    - [子组件向父组件要数据](#子组件向父组件要数据)
    - [slot](#slot)
    - [vue-cli](#vue-cli)
    - [开启debug模式](#开启debug模式)
    - [是否开启HTML5的history模式,开启后，需服务器端支持，否则报404](#是否开启html5的history模式开启后需服务器端支持否则报404)
    - [vue-router的钩子函数](#vue-router的钩子函数)

<!-- /TOC -->
## 学习目标
- 熟悉常见的vue.js框架的API
- 了解如何安装使用单文件组件
- 能自己完成todoMVC项目

## 学习建议
- 课程中使用的是v2.1.6版本
- 如果网上找的教程或书的代码执行不了，很正常，因为过时了

## 相关代码下载地址
[下载地址](https://github.com/black-pony/learn_vue_the_hard_way)

## 问题反馈
- 方式一：在博客下面留言
- 方式二：给我写邮件 js-class@qq.com

## 从angular 1.x中学到的概念review
### 框架与库的区别
库就是一堆的工具，比如我们使用了jQuery,但是并不能改变我们以往（第一步选择元素，第二步添加事件）的思路，只不过方便了我们写代码。
框架就是一套规则和规范，我们用了某框架之后，我们必须要按这套框架的规则去做，比如bootstrap,我们只要使用了bootstrap，我们按照它的教程定义一些class，就会得到一个响应式的页面。

###  SPA与多页面的区别

多页面应用就是一个网站里面，有一堆的页面，页面与页面之间是独立的，缺点就是当我们从一个页面跳转到另外一个页面的时候，另一个页面所有的东西全部需要从服务器加载，这样会出现白屏的现象，用户体验不好。
SPA就是single page application,单页面应用，比如我们打开网易云音乐，我们点击上面的链接会发现，页面并没有跳转，只不过是hash在发生改变，我们通过js监听hashchange事件，当触发的时候，我们就去服务器加载对应的数据，然后替换掉对应的DOM区域，但是页面的主体结构并不需要变动。

### mvc,mvvm
mvc就是把整个代码划分成模型、视图、控制器这三大块，模型负责管理数据（增删改查），视图就是我们的模板，控制器负责连接模型和视图。
1、view传送指令到controller
2、controller完成业务逻辑后，要求model改变状态
3、model将新的数据发送到view,用户得到反馈

mvvm是把整个代码划分成模型、视图、view model三大块：
mvvm采用双向数据绑定，view的变动，自动反映在view model，反之亦然。

### mvc和mvvm的作用：
1、解耦：让我们的代码结构比较清晰
2、便于我们的维护

### 如何安装angular.js
1、暴力安装
2、通过bower安装(淘汰了)
3、npm安装
4、cdn安装

### 数据绑定之单向数据绑定
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        div{
            width: 200px;
            height: 40px;
            line-height: 40px;
            outline: 1px solid green;
        }
    </style>
</head>
<body ng-app="myApp" ng-controller="myController">
    <!--当我们修改下面的div的值的时候，不会影响model里面message值-->
    <div contenteditable >{{message}}</div>
    <script src="./node_modules/angular/angular.js"></script>
    <script>
        window.onload= function(){
            document.getElementsByTagName("div")[0].focus()
        };
        var myApp = angular.module('myApp',[]);
        myApp.controller('myController',['$scope',function($scope){
            $scope.message = 'Hello world';
        }]);
    </script>
</body>
</html>
```
### 双向数据绑定
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        div{
            width: 200px;
            height: 40px;
            line-height: 40px;
            outline: 1px solid green;
        }
    </style>
</head>
<body ng-app="myApp" ng-controller="myController">
    <!--当我们修改下面的input的值的时候，会影响model里面message值-->
    <input type="text" ng-model="message">
    <div contenteditable >{{message}}</div>
    <script src="./node_modules/angular/angular.js"></script>
    <script>
        window.onload= function(){
            document.getElementsByTagName("input")[0].focus()
        };
        var myApp = angular.module('myApp',[]);
        myApp.controller('myController',['$scope',function($scope){
            $scope.message = 'Hello world';
        }]);
    </script>
</body>
</html>
```

### $watch

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        div{
            width: 200px;
            height: 40px;
            line-height: 40px;
            outline: 1px solid green;
        }
    </style>
</head>
<body ng-app="myApp" ng-controller="myController">
    <!--当我们修改下面的input的值的时候，会影响model里面message值-->
    <input type="text" ng-model="message">
    <script src="./node_modules/angular/angular.js"></script>
    <script>
        window.onload= function(){
            document.getElementsByTagName("input")[0].focus()
        };
        var myApp = angular.module('myApp',[]);
        myApp.controller('myController',['$scope',function($scope){
            $scope.message = 'Hello world';
            $scope.$watch('message',function(now,prev){
                console.log(now,prev);
            });
        }]);
    </script>
</body>
</html>
```
### filter过滤器
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        div{
            width: 200px;
            height: 40px;
            line-height: 40px;
            outline: 1px solid green;
        }
    </style>
</head>
<body ng-app="myApp" ng-controller="myController">
    <!--当我们修改下面的input的值的时候，会影响model里面message值-->
    {{'1484657346797'|date}}
    <ul>
        <li ng-repeat="item in arr | filter : {isTrue:true}">{{item.name}}</li>
    </ul>
    <script src="./node_modules/angular/angular.js"></script>
    <script>
        window.onload= function(){
            document.getElementsByTagName("input")[0].focus()
        };
        var myApp = angular.module('myApp',[]);
        myApp.controller('myController',['$scope',function($scope){
            $scope.arr = [
                {name:'itcast',isTrue:true},
                {name:'heima',isTrue:false},
                {name:'chuanzhi',isTrue:true},
                {name:'black-pony',isTrue:false}
            ];
        }]);
    </script>
</body>
</html>
```
### 指令
- ng-app
- ng-model
- ng-init
- ng-controller
- ng-bind
- ng-repeat
    + $index
    + $odd
    + $even
    + $first
    + $last
- ng-class
- ng-style
- ng-show
- ng-hide
- ng-if
- ng-switch
- ng-switch-when
- ng-src
- ng-href
- ng-bind-html(须引入ng-sanitize模块)

### 自定义指令

####  示例
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        div{
            width: 200px;
            height: 40px;
            line-height: 40px;
            outline: 1px solid green;
        }
    </style>
</head>
<body ng-app="myApp" ng-controller="myController">
    <input type="text" my-focus>
    <script src="./node_modules/angular/angular.js"></script>
    <script>
        var myApp = angular.module('myApp',[]);
        myApp.controller('myController',['$scope',function($scope){

        }]);
        myApp.directive('myFocus',function(){
            return {
                restrict:'A',
                link:function(scope,element,attributes){
                    element[0].focus();
                }
            };
        });
    </script>
</body>
</html>
```
#### 常见属性
- template
- templateUrl
- replace
- restrict
- transclude
- scope
- link

### ngRoute路由
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body ng-app="myApp">
    <div ng-view></div>
    <script src="./node_modules/angular/angular.js"></script>
    <script src="./node_modules/angular-route/angular-route.js"></script>
    <script>
        var myApp = angular.module('myApp',['ngRoute']);
        myApp.config(['$routeProvider',function($routeProvider){
            $routeProvider
                .when('/foo',{
                    template:'<h1>foo</h1>',
                    controller:'fooController'
                })
                .when('/bar',{
                    template:'<h1>bar</h1>',
                    controller:'fooController'
                })
                .otherwise({
                    template:'<h1>foo</h1>',
                    controller:'fooController'
                });
        }]);
        myApp.controller('fooController',['$scope',function($scope){

        }]);
        myApp.controller('barController',['$scope',function($scope){
            
        }]);

    </script>
</body>
</html>
```
### todoMVC的实现思路
- 本质上是进行数组的增删改查
- 显示 --> ng-repeat
- 删除 --> replace
- 修改 --> ng-class
- 增加 --> push

## vue基础知识

### 说明
- 本教程采用的是vue 2.1.9,请下载这个版本的进行学习，否则可能导致API用不了或过时
- 在学习阶段，不建议一上来就学习单文件组件模式

### 谁在用
- 阿里爸爸
- 饿了吗
- talking Data

### 安装
> npm init -y
>  npm install -S vue@2.1.9

### chrome相关插件
vue-dev tools
 
#### 使用注意
 一定要在服务器环境下面使用才能点亮这个插件
 
### visual studio code编辑器相关插件
- vue
- vue components
- vue 2 snippets
- vueHelper
- vetur
 
### vue的特点
-  简单轻量的js框架
- 数据驱动(自动追踪依赖的模板表达式和计算属性)
- 每个组件代表独立的单元、有各自的view及数据逻辑,用可解耦、可复用的组件来构造界面,你总是应该从UI出发抽象出不同的组件，然后像搭积木一样把它们拼装起来
- 最适合用来开发SPA
 
###  hello world
 
#### 示例
```html
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div id="myApp">
        <input type="text" v-model="message">
        {{message}}
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el:'#myApp',
            data:{
                message:'Hello world'
            }
        })
    </script>
</body>
</html>
```

### 讲解
- el --> 要绑定的元素，限定我们的vue项目的范围,这里可以用id，也可以用class，一般默认用id
- data --> 要绑定的数据模型
- {{message}} --> 插值表达式,可以用来获取我们的model中的数据
- new Vue() --> 每个vue项目都是通过构造器Vue来创建一个vue实例的
- v-model --> 类似ng-model,可以用来进行双向数据绑定
- data --> 我们的model

#### 注意事项
- vue不能挂载到body上面，会出现warnning警告

### 单次绑定
页面上的有些东西一旦赋值渲染之后，基本上不太可能会变动了，比如像我们的图片的url,像链接的href值，这个时候，我们可以使用单次绑定

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div class="myApp">
        <input type="text" v-model="message">
        <div v-once>
            {{message}}
        </div>
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el:'.myApp',
            data:{
                message:'Hello world'
            }
        })
    </script>
</body>
</html>
```

### 实现值加1
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div class="myApp">
        <input type="button" v-on:click="counter = (counter - 0) + 1" v-model="counter">
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el:'.myApp',
            data:{
                counter:1
            }
        })
    </script>
</body>
</html>
```

### 实现值加1升级版
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div class="myApp">
        <input type="button" v-on:click="add" v-model="counter">
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el:'.myApp',
            data:{
                counter:1
            },
            methods:{
                add:function(){
                    this.counter++;
                }
            }
        })
    </script>
</body>
</html>
```

### 为什么vue的性能这么高？
实现双向数据绑定，目前主要有三种方式：脏检查、观察机制、封装属性访问器

- 脏检查：框架将所有需要监控的属性放在一个队列中，当发生特定事件时，我们的框架只要觉得当前这个数据有可能变脏了，它就会遍历整个序列，对被监控的属性做对比，如果发生变化，则调用相应的处理函数。(angular实现了一套类似我们的原生的js的一套event loop)
angular 1.x的双向数据绑定是自己实现出来一套event loop机制，通过apply,watch list监听数据的变化，一旦它认为你的model变了，也就是变“脏”了，就去重新执行一轮event loop,进行脏值检测，所以效率很低。
![](http://ojmkbnynx.bkt.clouddn.com/17-1-17/33059309-file_1484661229826_df58.png)

- 观察机制：通过 Object.observe() 「已废弃」方法对对象进行监控，一旦其发生变化，将会执行相应的handler。
- 封装属性访问器：使用 Object.defineProperty 将对象的属性转换为 getter/setter ，当依赖项的 setter 被调用时，会通知 watcher 重新计算，从而致使它关联的组件得以更新。
vue.js使用的就是这种方式（当然不支持IE8）

### 双向数据绑定的原理
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div id="myApp">
        <input type="text" eric-model="message">
        <input type="text" eric-model="message">
        <div>
            <div>{{message}}</div>
        </div>
    </div>
    <script>
        var vm = {};
        Object.defineProperty(vm,'message',{
            val:null,
            get:function(){
                this.val = this.val || '';
                return this.val;
            },
            set:function(val){
                this.val = val;
                refresh_view();
            }
        });
        var el = document.querySelector('#myApp');

        //初始化视图
        function init_view(){
            var list = el.getElementsByTagName('*');
            var reg1 = /<.*>/g;
            var reg2 = /{{(.*)}}/;
            for(var i=0;i<list.length;i++){
                // console.log(list[i].innerHTML);
                if(list[i].tagName!='INPUT' && !reg1.test(list[i].innerHTML) && reg2.test(list[i].innerHTML)){
                    var myBind = reg2.exec(list[i].innerHTML)[1];
                    list[i].setAttribute('myBind',myBind);
                    // console.log(list[i].getAttribute('myBind'))
                    list[i].innerHTML = vm[list[i].getAttribute('myBind')];
                }
                if(list[i].tagName === 'INPUT' && list[i].getAttribute('eric-model')){
                    var myBind = list[i].getAttribute('eric-model');
                    list[i].value = vm[list[i].getAttribute('eric-model')];
                }
            }
        }

        init_view();

        function refresh_view(){
            var list = el.getElementsByTagName('*');
            for(var i=0;i<list.length;i++){
                if(list[i].getAttribute('myBind')){
                    list[i].innerHTML = vm[list[i].getAttribute('myBind')];
                }
                if(list[i].getAttribute('eric-model') && list[i].tagName === 'INPUT'){
                    list[i].value = vm[list[i].getAttribute('eric-model')];
                }
            }
        }

        var modelEleList = document.querySelectorAll('input[eric-model]');
        console.log(modelEleList);
        for(var i=0;i<modelEleList.length;i++){
            modelEleList[i].addEventListener('input',function(){
                var myBind = this.getAttribute('eric-model');
                vm[myBind] = this.value;
            },false);
        }

    </script>
</body>
</html>
```

### 表单控件
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div class="form-input">
    <span>message is {{message}}</span>
    <br>
    <input type="text" v-model="message">
  </div>
  <hr>
  <div class="form-chkbox">
    <input type="checkbox" id="checkbox" v-model="checked">
    <label for="checkbox">{{checked}}</label>
  </div>
  <hr>
  <div class="form-chkboxes">
   <input type="checkbox" id="jack" v-model="checkedNames" value="jack">
   <input type="checkbox" id="john" v-model="checkedNames" value="john">
    <br>
    message:{{checkedNames | json}}
  </div>
  <hr>
  <div class="form-radio">
    <label for="one">one</label>
    <br>
    <input type="radio" id="one" value="one" v-model="picked">
    <br>
    <label for="two">two</label>
    <input type="radio" value="two" v-model="picked">
    <br>
    <span>Picked:{{picked}}</span>
  </div>
  <hr>
  <div class="form-select">
    <select v-model="selected">
      <option>A</option>
      <option selected>B</option>
      <option>C</option>
    </select>
    <br>
    <span>selected:{{selected}}</span>
  </div>
  <script src="./node_modules/vue/dist/vue.js"></script>
  <script>
   new Vue({
     el:".form-input",
     data:{
       message:""
     }
   });
   new Vue({
     el:".form-chkbox",
     data:{
       checked:false
     }
   });
   new Vue({
     el:".form-chkboxes",
     data:{
       checkedNames:[]
     }
   });
   new Vue({
     el:".form-radio",
     data:{
       picked:''
     }
   });
   new Vue({
     el:".form-select",
     data:{
       selected:''
     }
   });
  </script>
</body>
</html>
```

### v-bind指令
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div id="myApp">
        <input type="text" v-bind="{id:myId,myAttr:myAttr,value:myValue}">
        <img v-bind:src="myImgSrc">
        <img :src="myImgSrc">
        <a v-bind:href="myUrl">百度</a>
        <a :href="myUrl">百度</a>
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el:'#myApp',
            data:{
                myId:'demo',
                myAttr:'demoAttr',
                myValue:'wfewf',
                myImgSrc:'http://i0.hdslb.com/bfs/archive/ac6ad98e868f313a332eb757634ddc9fcd5d7753.jpg@.webp',
                myUrl:'http://baidu.com',
            }
        });
    </script>
</body>
</html>
```
### watch监视
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div id="myApp">
       <input type="text" v-model="message1">
       <input type="text" v-model="message2">
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el:'#myApp',
            data:{
                message1:'hello1',
                message2:'hello2'
            },  
            watch:{
                message1:function(now,pre){
                    console.log(now,pre);
                }
            }
        });
        vm.$watch('message2',function(now,pre){
            console.log(now,pre);
        })
    </script>
</body>
</html>
```

### 计算属性
vue在2.1.5(大概这个版本，记不太清了)的时候，曾经取消了监视，因为作者发现，完全可以采用计算属性来实现：
#### 用计算属性替代监视
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div id="myApp">
       <input type="text" v-model="a">
       <input type="text" v-model="b">
       <input type="text" v-model="result">
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el:'#myApp',
            data:{
                a:0,
                b:0
            },  
            computed:{
                result:function(){
                    return Number(this.a) + Number(this.b);
                }
            }
        });
        vm.$watch('message2',function(now,pre){
            console.log(now,pre);
        })
    </script>
</body>
</html>
```
#### 用计算属性替代filter
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div id="myApp">
       <ul>
           <li v-for="item in arr1">{{item}}</li>
       </ul>
    </div>
    <script src="./node_modules/vue/dist/vue.js"></script>
    <script>
        var vm = new Vue({
            el:'#myApp',
            data:{
                arr:[2,3,4,5,6]
            },  
            computed:{
                arr1:function(){
                    return this.arr.filter(function(item){return item > 4});
                }
            }
        });
        vm.$watch('message2',function(now,pre){
            console.log(now,pre);
        })
    </script>
</body>
</html>
```

### v-bind:class
使用原则：静态的class放在HTML的class特效内，而动态的应该使用v-bind:class
```html
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="demo">
    <div v-bind:class="{red:isRed}">11</div>
    <div v-bind:class="{a,b}">111</div>
    <div v-bind:class="[c,{d:isD,e:isE}]">111</div>
    <!--绑定style-->
    <div v-bind:style="{fontSize:size + 'px'}">111</div>
    <div v-bind:style="{{width:'100px'},styleObjectB}">11</div>
  </div>
  <script src="./node_modules/vue/dist/vue.js"></script>
  <script>
    var app = new Vue({
      el:"#demo",
      data:{
        isRed:true,
        size:20,
        a:true,
        b:false,
        c:"world",
        isD:true,
        isE:true,
        styleObjectA:{
          color:'red',
          fontSize:'13px'
        },
        styleObjectB:{
          backgroundColor:'cyan'
        }
      }
    });
  </script>
</body>
</html>
```

### v-if,v-else
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="demo">
    <label for="one">one</label>
    <input type="radio" id="one" v-model="picked" value="one">
    <label for="two">two</label>
    <input type="radio" id="two" v-model="picked" value="two">
    <div v-if="picked==='one'">yes</div>
    <div v-else>No</div>
  </div>
  <script src="./node_modules/vue/dist/vue.js"></script>
  <script>
    var app = new Vue({
      el:"#demo",
      data:{
        picked:'one'
      }
    });
  </script>
</body>
</html>
```
### v-show
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="demo">
    <label for="one">one</label>
    <input type="radio" id="one" v-model="picked" value="one">
    <label for="two">two</label>
    <input type="radio" id="two" v-model="picked" value="two">
    <div v-show="picked==='one'">yes</div>
    <div v-show="picked!='one'">No</div>
  </div>
  <script src="./node_modules/vue/dist/vue.js"></script>
  <script>
    var app = new Vue({
      el:"#demo",
      data:{
        picked:'one'
      }
    });
  </script>
</body>
</html>
```

### v-for
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="demo">
    <!--数组的迭代-->
    <ul>
      <li v-for="(item,index) in arr">{{item}} - {{index}}</li>
    </ul>
    <!--对象的迭代-->
    <ul>
      <li v-for="(value,key) in obj">{{key}} - {{value}}</li>
    </ul>
    <!--vue特有的迭代-->
    <ul>
    <li v-for="n in 10">{{n}}</li>
    </ul>
  </ul>
  </div>
  <script src="vue.js"></script>
  <script>
    var app = new Vue({
      el:"#demo",
      data:{
        arr:[2,3,4],
        obj:{name:"eric zheng",sex:"male"}
      }
    });
  </script>
</body>
</html>
```

### v-cloak
配合[v-cloak] { display: none }使用，类似angular的ng-cloak

### 事件处理器 v-on
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="demo">
    <input type="button" v-on:click="fn" value="v-on:click点击触发">
    <input type="button" @click="fn" value="@click点击触发">
  </div>
  <script src="vue.js"></script>
  <script>
    var app = new Vue({
      el:"#demo",
      data:{
        arr:[2,3,4],
        obj:{name:"eric zheng",sex:"male"}
      },
      methods:{
        fn:function(){
          alert("被点击了");
        }
      }
    });
  </script>
</body>
</html>
```

### 事件对象event
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="demo">
    <input type="button" v-on:click="fn" value="v-on:click点击触发">
    <input type="button" @click="fn" value="@click点击触发">
  </div>
  <script src="vue.js"></script>
  <script>
    var app = new Vue({
      el:"#demo",
      data:{
        arr:[2,3,4],
        obj:{name:"eric zheng",sex:"male"}
      },
      methods:{
        fn:function(event){
          console.log(event.target);
        }
      }
    });
  </script>
</body>
</html>
```

### 修饰符
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="demo">
    <input type="button" v-on:click="fn" value="v-on:click点击触发">
    <!--相当于写了stopPropagation-->
    <input type="button" v-on:click.stop="fn" value="v-on:click点击触发">
    <!--相当于写了preventDefault-->
    <input type="button" v-on:click.prevent="fn" value="v-on:click点击触发">
    <!--既阻止冒泡还阻止事件默认行为-->
     <input type="button" v-on:click.prevent.stop="fn" value="v-on:click点击触发">
  </div>
  <script src="vue.js"></script>
  <script>
    var app = new Vue({
      el:"#demo",
      data:{
        arr:[2,3,4],
        obj:{name:"eric zheng",sex:"male"}
      },
      methods:{
        fn:function(event){
          console.log(event.target);
        }
      }
    });
  </script>
</body>
</html>
```

### 组件
我们在angular当中，可以通过自定义指令来实现在页面上自定义一些元素标签，但是在vue当中，是通过组件的形式来实现的,组件是vue最主要也是最强大的特性之一，它提供了HTML元素的扩充性，也将程序代码封装起来以便开发者重复使用。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="app">
    <custom-header></custom-header>
    <custom-main></custom-main>
  </div>
  <script src="./node_modules/vue/dist/vue.js"></script>
  <script>
   var app = new Vue({
     el:'#app',
     components:{
       CustomHeader:Vue.extend({
         template:'<div class="header">header组件</div>'
       }),
       CustomMain:Vue.extend({
         template:`
          <ul>
            <li><custom-block></custom-block></li>
            <li><custom-block></custom-block></li>
            <li><custom-block></custom-block></li>
            <li><custom-block></custom-block></li>
            <li><custom-block></custom-block></li>
          </ul>
         `,
         components:{
           CustomBlock:Vue.extend({
             template:'<h1>Hello world</h1>'
           })
         }
       })

     }
   });
  </script>
</body>
</html>
```
#### 组件使用注意事项
![](http://ojmkbnynx.bkt.clouddn.com/17-1-17/89984038-file_1484668060104_e92a.png)

### 子组件向父组件要数据
类似咱们angular中的自定义指令的scope
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div id="demo">
    <child :number="arr"></child>
  </div>
  <script src="./node_modules/vue/dist/vue.js"></script>
  <script>
    new Vue({
      el:"#demo",
      data:{
        arr:[2,3,4,5,6]
      },
      components:{
        child:Vue.extend({
          template:"<div><div v-for='item in number'>{{item}}</div></div>",
          props:{//props就是element上的attrs,换个名字property,变成复数 自定义属性的属性校验
            number:Array//这里指定需要的数据类型，如果写错了，控制台会有错误警告
          }
        })
      }
    });
  </script>
</body>
</html>
```

### slot
允许外部环境插入内容到组件的视图结构内
比如子组件为：

```html
<div>
    <h1>提示</h1>
    <slot name="content"></slot>
    <span>确定</span>
    <span>取消</span>
</div>
```

父组件使用子组件：

```html
<confirm>
    <p slot="content">HelloWorld</p>
</confirm>
```

最终的渲染完成的效果为：

```html
<div>
    <h1>提示</h1>
    <p>helloWorld</p>
    <span>确定</span>
    <span>取消</span>
</div>
```

### vue-cli
第一步、安装vue-cli npm install -g vue-cli
第二步、使用vue-cli初始化项目`vue init webpack-simple mydemo`
第三步、切换到vue项目当中
第四步、执行npm install
第五步、执行npm run build编译成功项目
第六步、执行npm run dev会自动开启项目在浏览器当中（默认是自动刷新的）

### 开启debug模式
```javascript
    Vue.config.debug = true;
```

### 是否开启HTML5的history模式,开启后，需服务器端支持，否则报404
```javascript
var router = new VueRouter({
    history:true
});
```

### vue-router的钩子函数
- beforeEach 在路由切换开始时调用
```javascript
router.beforeEach(function(){
    window.scrollTo(0,0);
});
```
- afterEach 在路由成功切换到激活状态时调用
```javascript
router.afterEach(function(transition){
    console.log(transition);
});
```
- router.redirect()  在找不到路由时跳转