---
comments: true
layout: post
title : 怎么使用grunt-tps
categories : 
- Stack
tags : 
- NodeJS
- Grunt
---


### grunt-tps是什么。

首先来说下TPS是什么，TPS的全称是Taobao Pictures System，中文意思就是淘宝图片系统，主要用于存放图片，当然也可以存放其他的东西。

而grunt-tps就是tps的grunt插件，基于tpsmate，只需要经过简单的配置，就可以用grunt进行自动化管理。

### 为什么要用grunt-tps

1. **自动化**，特别是当你的需要替换的目录是在一个文件夹下的，可以直接使用`xx/**/*`这样的方式。
2. 和grunt结合，grunt是个大趋势，使用grunt进行将平时一些反复劳动交给工具去做，提高工作效率。所有的事情，一行`grunt`搞定，简单轻松愉快。
3. 减少出错率，人工上传替换，难免会出现错误。

### tpsmate是什么？

TPS Mate是TPS系统的命令行版本。其中命令行版本基于python，当前功能主要包括上传单张图片、批量上传图片以及样式文件中背景图片的批量上传以及输出。其目的主要为减少手工替换以及为可能出现的前端打包工具提供更为有效的支持。

### 怎么安装tpsmate

首先要安装`python`，[http://www.python.org/download/]()


#### 使用tpsmate需要具备的条件：

1. 淘宝内部环境，需要可以访问tms.taobao.com
2. 有上传图片至tps的权限，看下你能否在[这里](http://tps.tms.taobao.com/photo/index.htm)上传图片

### 怎么使用grunt-tps

如果你以前从来没有用过[Grunt](http://gruntjs.com/)，推荐你看看Grunt的[Getting Start](http://gruntjs.com/getting-started)

如何安装grunt？

```haskell
    npm uninstall -g grunt
    npm install -g grunt-cli
```

接下来就是要安装grunt-tps
```haskell
    npm install grunt --save-dev
    npm install grunt-tps --save-dev
```

你的Gruntfile.js中加入这一段

```javascript
    tps: {
    options: {
        argv: "--inplace",
    },
    all: ['test.css', 'lib/**/*.css', 'test/**/*.scss','index.htm']
    }
```

你的Gruntfile.js中，看起来应该这样的

```javascript
    'use strict';
    module.exports = function (grunt) {
        // Project configuration.
        grunt.initConfig({
            // Configuration to be run (and then tested).
            tps: {
                options: {
                    argv: "--inplace"
                },
                all: ['test.css', 'lib/**/*', 'test/**/*.scss','index.htm']
            }
        });
        grunt.loadNpmTasks('grunt-tps');
        grunt.registerTask('default', ['tps']);
    };
```

- `argv`是tpsmate的参数，比如`--inplace`(用tps路径「线上路径」替换本地路径)，参考tpsmate的命令行方式

grunt-tps源码地址:[https://github.com/yize/grunt-tps]()

---
伊泽  
2013-5-28于杭州