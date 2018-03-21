---
title: postMessage的学习
date: 2017-11-07 12:26:00
tags:  [文章,JS]
---
这周接了个任务，要求页面内嵌iframe接入且需要与接入方通信，同事说可以尝试一下postMessage，于是就去学习了一下。
<!-- more -->
其实postMessage也挺有趣的，不仅仅是iframe，准确来说应该是两个站点之间跨域通信。
假设A、B两个站点，B站点设置了window的message事件监听，然后A站点向B站点发送信息，B站点即可收到，反过来也一样~

它的语法:

    otherWindow.postMessage(message, targetOrigin, [transfer]);
    
切记！targetOrigin只在开发环境里写成*方便调试，到生产环境的时候，为了确保安全（如直接发送密码），要设置成目标窗口的协议、主机地址或端口这三者匹配的targetOrigin值，消息才会被发送，防止被第三方截获。

PS.transfer是可选参数，和message一同发出，发出去的时候，所有权会随之转让（IE不支持的哦）

以iframe为例子

A站点:

    <!-- html -->
    <iframe src="B站点地址" id="test"></iframe>
    
    //script
    document.getElementById("test").contentWindow.postMessage({
        action: "test",
        msg: "test"
    }, '*');


B站点:
    
    win.addEventListener('message', function(e){
        var origin = event.origin || event.originalEvent.origin;
		if (origin=="A站点地址" && e.data.action == "test") {
			console.log('收到信息: '+e.data.msg);
		}else {
			alert('未知请求: '+ e.data.action);
        }
	})


看着很美好，瞬间实现了通信的功能，but...页面加载状态是个大问题...
实际测试的时候发现，A站点嵌入B站点的iframe，出现了B站点请求A站点，但是A站点还没加载完成导致miss了B站点的信息（iframe阻塞了父页面的加载）......蜜汁尴尬.......
另外，没有回调可言...虽然可以借助promise在发送和接收信息的时候改变状态实现回调，但这样还不如用ajax了~

whatever~编程在于折腾，尝试一下总不会错的~