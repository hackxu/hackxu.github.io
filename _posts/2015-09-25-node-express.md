---
layout: post
title: react mbe_ui浅析
description: "react"
tags: [mbe-ui, react]
comments: true
share: true
image:
  background: witewall_3.png
---

闲话不多说来正题

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
<!--more-->

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