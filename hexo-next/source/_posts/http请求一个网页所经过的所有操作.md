---
title: http请求一个网页所经过的所有操作
date: 2017-06-07 22:52:44
reword: true
comments: true
tags:
	- Http
	- 访问url的过程
categories:
	- Http
schedule:
	- 2017-06-07
keywords: http,url访问过程
description: 访问一个页面的全过程

---
### 一、自己的一个http请求的理解
1.Chrome搜索自身的DNS缓存
`chrome://net-internals/#dns`曾经浏览过的网站的dns
2.搜索操作系统自身的DNS缓存(浏览器没有找到缓存或缓存已经失效)
3.读取本地的HOST文件
4.浏览器发起一个DNS的一个系统调用
&emsp;4.1宽带运营商服务器查看本地缓存
&emsp;4.2运营商服务器发起一个迭代DNS解析的请求
&emsp;&emsp;``运营商服务器把结果返回给操作系统内核同时缓存起来``
&emsp;&emsp;``操作系统内核把结果返回浏览器``
&emsp;&emsp;``最终浏览器拿到了url对应的IP地址``
5.浏览器获得域名对应的IP地址后，发起HTTP"三次握手"
6.TCP/IP连接建立起来后，浏览器就可以向服务器发送HTTP请求了。
eg:用HTTP的GET方法请求一个根域名里的一个域名，协议可以采用HTTP1.0的一个协议。
7.服务器端接受到请求后，根据路径参数，经过后端的一些处理之后，把处理后的一个结果的数据返回给浏览器。如果是一个页面，就会把完整的HTML页面代码返回给浏览器。
8.浏览器拿到页面的完整HTML页面代码，在解析和渲染这个页面的时候，里面的JS和CSS、图片静态资源，它们同样也是一个个HTTP请求都需要经过上面的主要的七个步骤。
9.浏览器根据拿到的资源对页面进行渲染，最终把一个完整的页面呈献给用户。