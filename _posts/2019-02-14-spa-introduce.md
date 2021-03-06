---
layout:     post
title:      "web单页面应用"
date:       2019-02-14 15:00:00
author:     "monkey-yu"
header-img: "img/post-bg-mac.jpg"
catalog: true
tags:
    - 技术
---

#### 什么是单页应用

单页web应用，就是整个webapp 就一个html文件，里面的各个功能页面是javascript通过hash或者history api 来进行路由，并通过ajax拉取数据来实现响应功能。在应用整个使用流程里浏览器由始至终没有刷新，一切都由javascript 来控制。因此，单页web 应用会包含大量的JS代码，**模块化开发**和**架构设计**的重要性不言而喻。

#### 单页应用的优势

- **操作体验流畅**，媲美本地应用的感觉，切换过程中不会频繁有被“打断”的感觉。因为界面框架都在本地，与服务器的通讯基本只有数据，所以便于迁移，可以迁移成各种移动端Hybird产品。
- **完全的前端组件化，**前端开发不再以页面为单位，更多的采用组件化的思想，代码结构和组织方式更加规范化，便于修改和调整。
- **API共享，**如果服务是多端的，比如浏览器端、微信、Android等，单页应用的模式便于你在多端公用API,显著减少服务端工作量。因为容易变化的UI部分都前置到多端，只受业务数据模型影响的API更容易稳定下来。
- **组件共享，**可以在多端共享组件，便于产品的快速迭代，节约资源。

#### 单页应用的缺点

- **首次加载大量资源。**要在一个页面上为用户提供产品的所有功能，在这个页面加载的时候，首先要加载大量的静态资源，这个加载时间较长
- **对搜索引擎不够友好**，因为界面大部分是动态生成的，所以搜索引擎不容易索引它
- **开发难度相对较高，**开发者的js技能需过硬，并且需要组件化、设计模式有所认识。

#### 开发框架

为解决大规模单页应用代码逻辑问题，出现不少MV*(MVC、MVP、MVVM)框架，他们的基本思路都是在js层创建模块分层和通信机制，为单页应用开发提供必需的模板、路径解析和处理、后台服务api访问、DOM操作等功能。这类框架包含Vue、AngularJS、Backbone等，他们几乎都在这些模式上产生了变异。

框架能极大的提高我们开发的便利，但是框架一般都限制过多。

#### 代码隔离

单页应用比页面型网站更加依赖于js,各种子功能的js代码聚集到同一个作用域下，所以代码的隔离、模块化很重要。

#### 代码合并与加载策略

- 把更多的公共功能放到首次加载，以减少每次加载的载入量
- 在单页面应用中，无需想网站型产品一样，为了防止文件加载阻塞渲染，把js放到html后面加载，因为它的界面基本是动态生成的。

#### 路由与状态的管理

单页面应用中，因为界面上的各种功能区块是动态生成的，所以需要把产品功能划分为若干状态，每个状态映射到相应的路由，然后通过根据不同的url路径动态解析路由，匹配功能界面。

#### 缓存与本地存储

- 在单页应用中，缓存是很重要的环节
- 由于这类系统的前端部分几乎全是静态文件，所以它能够有机会利用浏览器的缓存机制，而比如动态加载的界面模板，也完全可以做一些自定义的缓存机制，在非首次的请求中直接取缓存的版本，以加快加载速度。
- 业务代码也常常会需要跟本地存储打交到，存储一些临时数据，可以使用localStorage 和localStorageDB来简化自己的业务代码

#### 服务端通信

- 传统的web产品通常使用JSONP和AJAX这样的方式来与服务端通信，但在单页应用中，很大一部分裁员WebSocket这样的实时通讯方式。
- WebSocket与传统基于HTTP的通信机制相比，有很大的优势。它可以让服务端很便利地使用反向推送，前端只响应确实产生业务数据的事件，减少一遍又一遍无意义的AJAX轮询。
- 由于WebSocket只在比较先进的浏览器上被支持，有一些库提供了在不同浏览器中的兼容方案，比如socket.io，它在不支持WebSocket的浏览器上会降级成使用AJAX或JSONP等方式，对业务代码完全透明、兼容。



