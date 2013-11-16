---
comments: true
layout: post
title : cubieboard问题汇总
description : cubieboard是什么，能用来干什么,怎么用cubieboard做服务器
categories : 
- Stack
tags : 
- Cubieboard
---


## Cubieboard
1. Cubieboard是什么？  

	Cubieboard是一个又小（10x6 厘米）又强大的[ARM](http://zh.wikipedia.org/wiki/ARM%E6%9E%B6%E6%A7%8B)开发板，它搭载了Allwinner [A10](http://linux-sunxi.org/A10)( Cortex-A8 )单芯片，特点：黑客友好，可扩展，成本非常低。  
	通俗的说，就是一台搭载arm CPU的电脑
	目前淘宝价格￥379.
1. 板子配置是怎样的？
	
	* 1G ARM cortex-A8处理器, NEON, VFPv3, 512KB二级缓存
	* Mali400, OpenGL ES GPU
	* 1GB DDR3 @ 480MHz
	* HDMI 1080p高清输出
	* 100M USB以太网口
	* 4GB Nand Flash
	* 2 USB Host, 1 MMC slot, 1 SATA, 1 ir
	* 96个扩展pin,支持  i2c, spi, lcd和红外传感器, ..
	* 运行Android, Ubuntu或其他Linux版本
	
1. Cubieboard和Raspberry Pi 有关系吗？

	没有关系，网上说是Raspberry Pi的加强版，那只是宣传手段而已，Raspberry Pi是国外团队搞的，Cubieboard是国内团队搞的。
	Cubieboard是国货，是由汤亮（Tom Cubie）领导的团队在indiegogo上集资后开发的
	
	Cubieboard和Raspberry Pi的[对比](http://just4fun.cn/?cat=73)
	
	Cubieboard大约比树莓派快大约3到2倍的样子
	
1. Cubieboard可以用来干嘛？

	适合纯粹玩系统或用来影音娱乐,拥有1080p的HDMI输出口  
	cubieboard只有网口没有网卡（也就是没有network controller），所有的收包解包都由CPU完成，所以能支持的流量比较有限，不过撑个10万的闲链接还是没问题的。
还想了解一下cubieboard对https的支撑能力，于是在cubieboard上装了tengine，配上https签名再用ab压力测试，ab压测脚本是：

```haskell
ab -n 20000 -c 20 -k url
```

测试结果：访问https的QPS为`755`, 访问http的QPS为`1269`

用cubieboard搭个小网站是绰绰有余的，一个小的聊天服务器兴许也可以。

	
	
1. 目前支持的系统

	* android
	* xbmc
	* linaro
	* ubuntu
	* archlinux
	* freebsd
	
1. 利用动态域名解析服务，将cubieboard作为服务器。

	可以参考[这篇文章](http://cn.cubieboard.org/forum.php?mod=viewthread&tid=189&extra=page%3D2%26orderby%3Dlastpost)
	
	推荐学习资料[http://cb.e-fly.org/](http://cb.e-fly.org/)