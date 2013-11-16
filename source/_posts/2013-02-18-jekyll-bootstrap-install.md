---
comments: true
layout : post
title: jekyll-bootstrap安装
description : 用jekyll-bootstrap安装，打造免费的github+jekyll+bootstrap博客。修改convertible.rb解决utf-8导致的jekyll服务无法启动
categories : 
- Stack
tags : 
- Jekyll
- Bootstrap
- Github
---

安装jekyll-bootstrap

### 首先需要安装jekyll  [官网wiki](https://github.com/mojombo/jekyll/wiki/install)：

1. ruby1.9.1-dev中包含gem的安装包

```haskell
sudo apt-get install ruby1.9.1-dev
```

2. 安装jekyll

```haskell
sudo gem install jekyll
```
### 接下来需要花3分钟完成jekyll-bootstrap的安装 (将USERNAME替换为你的github的用户名)


1. 建立新的项目

    去你的 [https://github.com](https://github.com) 建立一个名为USERNAME.github.com的项目

2. 安装Jekyll-Bootstrap
```haskell
$ git clone https://github.com/plusjade/jekyll-bootstrap.git USERNAME.github.com
$ cd USERNAME.github.com
$ git remote set-url origin git@github.com:USERNAME/USERNAME.github.com.git
$ git push origin master
```
3. 等待几分钟，去看下你的 [http://USERNAME.github.com](http://USERNAME.github.com)

### *如果你已经有了一个你的github博客，你可以在本地启你的jekyll服务：

```haskell
$ git clone https://github.com/plusjade/jekyll-bootstrap.git
$ cd jekyll-bootstrap
$ jekyll --server
```
去看下[http://localhost:4000](http://localhost:4000).

中文下，请将文件改为`utf-8`格式，如果GBK可能会出现jekyll服务无法启动的错误

解决方法：

修改jekyll为默认打开utf-8：

1. 找到convertible.rb

```haskell
sudo find / -name convertible.rb
```
我的是在`/var/lib/gems/1.9.1/gems/jekyll-0.12.0/lib/jekyll/convertible.rb`

```haskell
cd /var/lib/gems/1.9.1/gems/jekyll-0.12.0/lib/jekyll/ && sudo vim convertible.rb
```

2. 将`self.content = File.read(File.join(base, name)` 改为 `self.content = File.read(File.join(base, name), :encoding => 'utf-8')`

参考资料：

- [https://help.github.com](https://help.github.com/)

- [https://github.com/mojombo/jekyll/wiki/install](https://github.com/mojombo/jekyll/wiki/install)

- [http://jekyllbootstrap.com/](http://jekyllbootstrap.com/)