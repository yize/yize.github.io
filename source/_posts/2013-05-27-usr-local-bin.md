---
comments: true
layout: post
title : 恢复mac下的/usr/local/bin
categories : 
- Stack
tags : 
- Shell
- Mac
---


今天一早配置phpstorm的时候，看到文件上有很多warn，比如，require不存在这样。

然后就开始坑爹的瞎搞了，点了`external libraries`里，添加了`/usr/local/bin/node`

发现还是有warn报错，随之，看是悲剧的一步，虽然我是想删除external libraries中对node的引用，删除的时候，有红色的提示，没管那么多，直接跳过去了。。。

发现不对，在`terminal`中，各种`node`,`git`这样的命令没用了。

用sudo也是没有权限。

后来同事提醒，可能是权限问题。

查了下此时的/usr/local/bin下的文件，现在都是在我的名下，group也在admin下。

试了下重新安装node，发现，node在root名下，group是wheel。

并且是有`x`权限的。

解决方法如下：
```haskell
	sudo chmod -R +x /usr/local/bin/
	sudo chown -R root /usr/local/bin/
	sudo chgrp -R wheel /usr/local/bin/
```
如此，解决。


---
伊泽  
2013-5-27于杭州