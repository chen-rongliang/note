---
title: event.srcElement与event.target的区别
date: 2017-11-01 15:00:23
tags: [文章,JS]
---
起初不知道这玩意是啥，看到的时候是别人写的原生事件委托时用到，大约猜到是和event.target类似的兼容写法，好奇就度娘搜了一下。
<!-- more -->
其实就是字面的意思，event的源元素，通过它可以进行和document.getElementById(element)一样的操作。

![此处输入图片的描述][1]

我们在一个输入框失焦的时候alert一下值

    html：
    <input type="text" onblur="test()">

    JS:
    var test = function(){
        var e = e || window.event;
        var target = e.target || e.srcElement;  //for IE~
        alert(target.value);
    }


  [1]: https://ss0.bdstatic.com/94oJfD_bAAcT8t7mm9GUKT-xh_/timg?image&quality=100&size=b4000_4000&sec=1509520034&di=4695ca495133601f99d9a04729955a7e&src=http://img.mp.sohu.com/q_mini,c_zoom,w_640/upload/20170708/b889681e1c7e471f8f58a0799585811a.jpg
