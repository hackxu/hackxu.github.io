---
layout: post
title: 第一次接触ng todoList，产出物
description: "ng"
tags: [ng, todolist]
image:
  background: witewall_3.png
comments: true
share: true
---

# 简介

听说ng很屌 ，今天看了看，顺便写了个简单的web 应用程序

## 为什么需要ng？

类似 Backbone 或者 JavaScriptMVC，anguar是一个快速的前端开发解决方案。没有其它的插件或者架构足以开发数据驱动的web应用。下面列出了AnguarJS的一些特性：

方便的REST： RESTful逐渐成为了标准的服务器和客户端沟通的方式。使用一行javascript代码，你就可以快速的从服务器端得到数据。AugularJS将这些变成了JS对象，作为Model，遵循MVVM(model view view-model)设计模式。

MVVM救星：Model将和ViewModel互动（通过$scope对象），将监听Model的变化。这些可以通过View来发送和渲染，由HTML来展示你的代码。View可以通过$routeProvider对象来支配，所以你可以深度的链接和组织你的View和Controller，将他们变成导航URL。AngualrJS同时提供了无状态的Controller，可以用来初始化和控制$scope对象。
<!--more-->

数据绑定和依赖注入：在MVVM设计模式中的任何东西无论发生任何事情都自动的和UI通信。这帮助我们去除了wrapper，getter/setter方法或者class定义。AngularJS将帮助我们处理所有的这些内容，所以你可以处理数据像处理基本javascript数据类型，例如，数组一样简单。当然你也可以通过自定义处理复杂数据。正因为所有事情的发生都是自动的，所以你不必调用一个main()来执行你的代码，而是通过依赖关系来驱动。

可扩展的HTML：大多数的网站都是使用非语义的<div>标签来搭建的。你需要自己在CSS的class中定义相关的DOM层次结构。而使用AngularJS，你可以操作XML一样操作HTML，给你无穷的方式来完成标签和属性定义。AngularJS通过自己的编译器和directives来完成相关的设置。

使用HTML模板：如果你曾经使用过Mustache ， Hogan.js，或者handlerbars的话，你就可以快速的理解AngularJS的模板引擎语法，应为它是纯HTML的。AngularJS通过DOM浏览来完成此类功能，使用上面提到的directives。模板被作为DOM元素传递到Angular的编译器中，可以被扩展，执行或者重用。这很关键，这样一来你就拥有了DOM组件，而非字符串，允许你直接的操作扩展DOM树。

企业级别的测试：AnguarJS并不依赖于第三方的插件或者是框架，包括测试。如果你熟悉QUnit, Mocha 或者 Jasmine的话，那么对于理解Angular的单元测试和Scenario Runner来说就非常简单。

以上的这些基本的原则能够帮助知道你使用Angular来创建高效性能可维护的代码。只要你有代码保存数据，AnguarJS会帮助你处理所有的重量级内容，提供一个富客户端的超棒体验！


# 问题
表示开始的时候还遇到一些问题，提交两次相同的内容ng就会报错，百度了一下是这样写的 `track By $index `，结果一直报错 最后谷歌了一下` By`的`B`其实是小写的。。不是故意黑百度的，
缺少的js和css请自行下载引用更换路径
# 代码

源码如下

{% highlight JavaScript %}

<!DOCTYPE html>
<html lang="en" ng-app="todoList">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
    <meta name="format-detection" content="telephone=no"/>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0">
    <title>TODOLIST</title>
    <!-- Latest compiled and minified CSS -->
    <style>
        .list-group li{ display: block; overflow: hidden;}
        .right{
            float: right;
            margin-right: 10px; display: block; cursor: pointer;}
    </style>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
</head>
<body ng-controller="TaskCtrl" style="padding: 10px;">
<div class="input-group">
    <input type="text" ng-model="task" class="form-control"/>
    <span class="input-group-btn">
        <button class="btn btn-default" ng-click="add()">提交</button>
    </span>
</div>
<h4 ng-if="tasks.length>0">任务列表</h4>
<ul class="list-group">
    <li ng-repeat="item in tasks track by $index" class="list-group-item">{{item}}
        <a ng-click="tasks.splice($index,1)" class="right">删除</a>
    </li>
</ul>
<script src="../js/angular.min.js"></script>
<script>
    angular.module('todoList',[])
            .controller('TaskCtrl',function($scope){
                $scope.task="";
                $scope.tasks=[];
                $scope.add= function(){
                    $scope.tasks.push($scope.task);
                }
            })
</script>
</body>
</html>
{% endhighlight %}



<strong>本文原创</strong>
