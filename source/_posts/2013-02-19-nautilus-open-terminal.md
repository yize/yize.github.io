---
comments: true
layout: post
title : ubuntu下右键在终端中打开
description : ubuntu下，在GUI中浏览文件的时候，有时候需要用到terminal打开当前目录，比较好用的方法是安装nautilus-open-terminal
categories : 
- Stack
tags : 
- Linux
- Terminal
---

ubuntu下，在GUI中浏览文件的时候，有时候需要用到terminal打开当前目录，之前的做法是一路cd下去。。
这未免也太浪费时间了。
有没有快捷的方法呢？百之谷之，得此：

```haskell
nautilus-open-terminal
```
1. 安装nautilus-open-terminal

```haskell
sudo apt-get install nautilus-open-terminal
```
2. 重启X


`right Alt + Printscreen + K`