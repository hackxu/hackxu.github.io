---
layout: post
title: node express初学
description: "node"
tags: [node, express]
comments: true
share: true
image:
  background: witewall_3.png
---

##还是先来扯扯node的优缺点吧

### 处理高并发场景性能更高

在用 http://socket.io 之前，推送服务是用 ajax polling 做的。我们用 Tornado 和 Node.js 做过两个版本的推送服务。在当时的测试环境下，Node.js 的 CPU 时间是 Tornado 的三分之一，内存使用是 Tornado 的一半，代码行数只有 Tornado 的三分之一（Node.js 版是用 coffee 写的）。后来我们使用了 http://socket.io，CPU 开销进一步降低。

### 函数式编程非常适合写异步回调链

用 Node.js 配合 CoffeeScript 写异步操作链非常便利，相比之下 Tornado 无论是写命名函数的回调，还是 yield 一个 Task 都没那么自然。

<!--more-->

###缺点：

1. 大量匿名函数使异常栈变得不好看。
2. 无法以 request 为单位 catch 异常，必须确保不要在不 catch 异常的第三方库的回调里的抛异常，这在一个异步操作链条里是一件比较麻烦的事。解决方法之一是对那些不 catch 异常的第三方库做一些封装，把所有的异常变成事件，改成 on('error') 形式的 API。


##node的安装

node可以去官网下载安装包这个就不多说了，安装完node之后可以通过 `node -v` 查看当前版本号。安装express的话，如何是4.0的版本最好使用 `npm install -g express-generator` 安装。
这里的 `-g` 是全局global的意思，一般来说还是全局安装的好，因为安装的时候已经帮你配置好了系统的环境变量。

##关于package.json

package.json的代码通常是这样的

{% highlight JavaScript %}

  {  
    “name”: “helloexpress”,  
    “description”: “hello express!”,  
    “version”: “0.0.1”,  
    “private”: true,  
    “dependencies”: {  
      “express”: “4.x”  
    }  
  }  

{% endhighlight %}

看起来跟普通的json没什么区别，但是在这里区别却很大。 dependencies是所需要安装的node模块，通常在项目根目录建立，也可以通过命令 `npm init`来建立。当有package.json存在的时候，就可以通过`npm install`来安装所需要的依赖模块。是不是很方便呢！

##重头戏app.js

直接贴代码
{% highlight JavaScript %}

 var express = require(‘express’);  
 var app = express();  
    
 app.get(‘/’, function(req, res){  
   res.send(‘hello express’);  
 });  
    
 app.listen(3000);  

{% endhighlight %}

如上所示就是app.js的代码了，当执行`node app.js`的时候，俺们就能在浏览器的地址栏输入http://127.0.0.1:3000/ 来看到我们的效果 hello express，这是node的重点，这段代码
就是在起了一个本地服务器，hah，（为什么不是传统的hello world呢，因为俺不识字）