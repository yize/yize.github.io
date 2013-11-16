---
comments: true
layout: post
title : env node\r No such file or directory
categories : 
- Stack
tags : 
- NodeJS
---


env: node\r: No such file or directory

uitest是基于nodejs的，用`npm install uitest -g`安装完之后，在mac下运行，提示`env: node\r: No such file or directory`，检查了下bin文件中，第一行是

```haskell
#! /usr/bin/env node
```
这看起来是没有任何问题的，当然是肉眼看起来。

问题的分析：

env：node\r 

注意下这里的\r，好眼熟，是个换行，原谅我对DOS不是很了解。。。

google了下发现找到了[这个](https://github.com/foglcz/tscw/issues/1)

里面提到，用dos2unix转换下就可以了。

我的机器上没装dos2unix，用brew装了个

```haskell
brew install dos2unix
```
接着cd到 bin目录下

```haskell
sudo dos2unix uitest
```
就可以了

---
伊泽  
2013-5-18于杭州