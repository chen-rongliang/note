---
title: 针对html元素的全屏实现
date: 2017-10-26 14:12:14
tags: [文章,JS]
---

这是个很棒的功能。一般我们都是直接针对网页来实现，等同与F11的功能。
<!-- more -->
但是今天发现个好玩的，可以针对某元素实现全屏⊙_⊙
这就很6了，有了它我们就能实现类似元素视觉聚焦，如HTML5全屏等╮(╯▽╰)╭
**实现原理，主要靠浏览器提供的API支持**

首先是w3c标准的

    // 全屏
    element.requestFullScreen();
    // 退出全屏
    document.exitFullscreen();


而各家浏览器的私有支持的

    // Chrome
    document.webkitCancelFullScreen();
    // 火狐
    document.mozRequestFullScreen();


这情况嘛，当然是做兼容处理啦~

    //  做个全屏的构造函数
    var FullScreen = function(elem){
      this.elem = document.querySelector(elem);
    }
    //  全屏
    FullScreen.prototype.in = function() {  
        if (this.elem.requestFullscreen) {
          this.elem.requestFullscreen();
        } else if (this.elem.webkitRequestFullscreen) {
          this.elem.webkitRequestFullscreen();
        } else if (this.elem.mozRequestFullScreen) {
          this.elem.mozRequestFullScreen();
        } else if (this.elem.msRequestFullscreen) {
          //  IE的实现没有实测过，不过据网上的资料说IE11以下可实现的
          this.elem.msRequestFullscreen();
        }
    }
    //  退出全屏
    FullScreen.prototype.out = function() {  
        if (document.exitFullscreen) {
          document.exitFullscreen();
        } else if (document.webkitExitFullscreen) {
          document.webkitExitFullscreen();
        } else if (document.mozCancelFullScreen) {
          document.mozCancelFullScreen();
        } else if (document.msExitFullscreen) {
          document.msExitFullscreen();
        }
    }


当我们使用的时候，new一个就好了

    var test = new FullScreen(".test");
    //  全屏
    test.in();
    //  退出
    test.out();

补充说明，测试过程中发现个bug：元素全屏和网页全屏(F11)的退出会冲突...暂时思路是在元素屏蔽的期间屏蔽网页全屏的键盘事件
