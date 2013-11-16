---
comments: true
layout: post
title : 前端编码问题汇总
categories : 
- Stack
tags : 
- JavaScript
---


## 前端可能会遇到的编码问题有哪些？

1. 文件编码，GBK，注意IDE编码，不要默认转换UTF-8.
1. 文件中内容的编码，可以将内容手动转成UTF-8编码或者unicode
1. scss中编码，解决方法，在scss头部加入 `@charset "GBK"`
1. 请求时的中文编码，淘宝规范在请求后加入 `_input_charset=utf-8`
1. "<>"等直接输出的，应该用`&lt；`,`&gt；`这样的转义符号
1. 如果直接读取用户输入的字符，应该用`encodeURIComponent`,`htmlspecialchars`等编码
1. JS引入的时候，带上`charset`，指定文件的编码
1. HTML页面中，`meta`指定`charset`,HTTP解析的时候，有三个地方可以埋藏代码信息：
	
	1. http头的Content-Type
	1. html页面中的meta标签中制定的charset
	1. 页面正文数据（浏览器可以跟进二进制码来判断编码）

> 如果三者编码不一致，浏览器会首先读取http头中的content-type，若没有设定编码，再查找页面中meta标签中的charset设定，如果还没有就以浏览器默认编码来显示，如果默认编码没有指定，浏览器会通过解析正文内容来判断编码.所以，页面是gbk编码，即便meta属性中设置 charset=utf-8，只要content-type中设定为gbk（或者GB2312、GB18030），该页面就正常显示，如果这时没有设定 content-type的编码，浏览器就会以meta中的charset属性为准，页面出现乱码。
		
		
1. JSONP中的中文问题，解决方法，后端返回`unicode`编码。
1. nodejs中的编码问题，可以使用`iconv`解决，或者直接用`buffer`