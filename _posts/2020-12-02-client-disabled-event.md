---
layout:     post
title:      "禁止文字选中、禁止网页拖拽等事件"
date:       2020-12-02 12:00:00
author:     "monkey-yu"
header-img: "img/tree.jpg"
catalog: true
tags:
    - 浏览器
---

#### 1. html中禁止文字选中

user-select:  none | text | all | element

取值：

none :  文本不能被选择

text ： 可以选择文本

all: 当所有内容作为一个整体时可以被选择

**说明：**

1.IE6-9不支持该属性，但支持使用标签属性 **`onselectstart="return false;"`** 来达到 `user-select:none` 的效果；Safari和Chrome也支持该标签属性；

2.直到Opera12.5仍然不支持该属性，但和IE6-9一样，也支持使用私有的标签属性 **`unselectable="on"`** 来达到 `user-select:none` 的效果；unselectable 的另一个值是 off；

3.除Chrome和Safari外，在其它浏览器中，如果将文本设置为 `-ms-user-select:none;`，则用户将无法在该文本块中开始选择文本。不过，如果用户在页面的其他区域开始选择文本，则用户仍然可以继续选择将文本设置为 `-ms-user-select:none;` 的区域文本；

4. 例子

   ```html
   <!DOCTYPE html>
   <html lang="en">
       <head>
           <meta charset="UTF-8">
           <meta http-equiv="X-UA-Compatible" content="ie=edge">
       </head>
       <style>
           .test {
               padding: 10px;
               -webkit-user-select: none;
               -moz-user-select: none;
               -o-user-select: none;
               user-select: none;
               background: #eee;
           }
       </style>
       <body>
           <div class="test" onselectstart="return false;" unselectable="on">禁				止选中文本内容
           </div>
       </body>
   </html>
   ```

#### 2. 禁止网页拖拽等事件

```html
<body 
      οncοntextmenu="return false" 
      οndragstart="return false" 
      onselectstart="return false">
</body>
```

οncοntextmenu: 取消鼠标右键

ondragstart: 禁止鼠标在网页上拖动

onselectstart:  禁止选择网页中的文字

#### 3. window.event 的属性

属性有：

```
altKey, button, cancelBubble, clientX, clientY, ctrlKey, fromElement, keyCode, offsetX, offsetY, propertyName, returnValue, screenX, screenY, shiftKey, srcElement, srcFilter, toElement, type, x, y
```

其中returnValue :

设置或检查从事件中返回的值。 true 事件中的值被返回；false 源对象上事件的默认操作被取消

下面代码同2：

```html
<body 
      οncοntextmenu="window.event.returnValue = false" 
      οndragstart="window.event.returnValue = false" 
      onselectstart="window.event.returnValue = false">
</body>
```

