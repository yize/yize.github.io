---
comments: true
layout: post
title : 尝试使用Tengine(nginx)
description : 使用Tengine(nginx)，打造本地combo服务器，方便前端本地开发，淘宝内部前端环境配置
categories : 
- Stack
tags : 
- Linux
- Nginx
---


最近这几天信息量比较大，接触了很多的东西，学了很多，先不说学习方法问题，至少个人在成长。

今天和
<a wb_screen_name="淘宝道璘" href="#">@淘宝道璘</a>
一起在玩Tengine

想要做的事情是从apache换到Tengine，道璘之前有研究过nginx，他说：在windows上，nginx存在两个问题，一个是中文路径，两外一个是php不稳定。后来还是切回了apache。

直接用起公司开源的Tengine [Github](https://github.com/taobao/tengine)

## 普通安装模式

因为需要支持combo，也就是`http://example.com/??style1.css,style2.css,foo/style3.css`的格式，所以安装流程是这样的：

```haskell
git clone git://github.com/taobao/tengine.git
cd tengine
```


然后编译之后安装

```haskell
./configure --with-http_concat_module
make
sudo make install
```
如果不需要支持combo的话，就不需要带`--with-http_concat_module`参数。

装完以后当然要开始配置。(`配置本地代理，也就是assets.daily.taobao.net等指向本地文件夹`)

```haskell
sudo vi /usr/local/nginx/conf/nginx.conf
```
在httpd中添加

```haskell
server {
    listen  80;
    server_name assets.daily.taobao.net a.tbcdn.cn; #改成自己的assets_server
    concat on; #打开concat
    root /home/pofa/work/assets/; #本地assets路径，需要改成自己的assets_path
    autoindex on;
    error_page 404 = @ucool; #淘宝ucool，如果文件不存在，从ucool取
    location @ucool{
        proxy_set_header Host $http_host;
        proxy_pass http://10.232.39.168;
    }
}
```

## 是不是觉得比较麻烦？启用屌丝模式！

```haskell
git clone git://github.com/yize/tengine.git
cd tengine
```

`注意：请先备份自己的/usr/local/nginx/conf/nginx.conf哦！！`

然后sh下

```haskell
sh ./tengine-combo.sh #需要concat模块
or
sh ./tengine.sh #不需要concat模块
```
好了之后别忘了在`/etc/hosts`中增加127.0.0.1 assets.daily.taobao.net a.tbcdn.cn

如果不想用本地代理的话，注释掉hosts中上面这一句就行了

enjoy it!

源码在我的[GITHUB](https://github.com/yize/tengine)上