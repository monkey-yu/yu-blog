---
layout:     post
title:      "vue项目打包后如何本地运行"
date:       2020-11-04 12:00:00
author:     "monkey-yu"
header-img: "img/post-bg-mac.jpg"
catalog: true
tags:
    - Vue
---

#### 前言

我们知道在使用Vue官方给出的脚手架vue-cli搭建的项目，默认是有2个脚本功能的：

- npm run serve 允许你本地启动这个项目
- npm run build 将整个项目进行压缩构建到dist这个目录下，即打包

#### 正文

##### 1.默认的打包情况

通常情况下，打包后的dist文件夹我们不需要本地访问。通常是会将该文件夹放在服务器上,或者映射路径下，启动你的服务器即可，然后就可以使用你配置的路径访问到项目。

看看默认情况下打包出的index.html:

![dist-old](/img/post_img/vue/dist-old.png)

可以看到上述的路径是这样的绝对路径。

`vue-cli`中对于`publicPath`这个属性的配置是默认为`'/'`(也就是整个项目的根目录)。

以这个项目根目录为基准的, 但是这个项目根目录并没有我们要的`css、js、image`等文件夹呀, 这些文件夹是在`dist`文件夹里面!!!

##### 2.配置修改后的打包情况

上述说的是通常情况，然而另一种情况就是需要你本地浏览器打开dist/index.html 可访问，而不是空白。
首先上结果，看看修改配置后打包出的index.html:
![dist-new](/img/post_img/vue/dist-new.png)

第一步：配置`vue-cli`中对于`publicPath`这个属性

如果项目里有webpack的配置文件，可以直接修改：

![dist-3](/img/post_img/vue/dist-3.png)

将`build`对象下的`assetsPublicPath`中的`“/”`，改为`“./”`即可。

然而基于vue-cli 2或vue-cli3中，可能找不到webpack的配置文件。不过vue-cli也提供了一个入口可以修改webpack配置。

即在根目录下新建一个vue.config.js，然后修改其中的`publicPath`这个选项：

![dist-4](/img/post_img/vue/dist-4.png)

将这个选项设置为`'/'`(当前文件夹)。

这时候本地打开dist文件夹中的index.html 就可以了。

如果有使用vue-router 的话，需要配置第二步。

 第二步：将router 的模式设置成hash模式。

![dist-5](/img/post_img/vue/dist-5.png)

把这里注释就可以了，因为mode默认就是hash模式。

到此，打包出来的文件本地浏览器可以访问啦！
