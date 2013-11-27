---
layout: post
title: "zsh下rake new_post[\"title\"] 报错的问题"
date: 2013-11-27 09:38
comments: true
categories:
- Stack
tags:
- Ruby
- Octopress
- Zsh
---

```haskell
rake new_post["title"]   
zsh: no matches found: new_post[title]
```

在`zsh`中使用`rake new_post`的时候抛出找不到匹配的异常，原因是

[zsh官方文档](http://zsh.sourceforge.net/Doc/Release/Expansion.html#Filename-Generation)中有这样的说明：

> If a word contains an unquoted instance of one of the characters ‘*’, ‘(’, ‘|’, ‘<’, ‘[’, or ‘?’, it is regarded as a pattern for filename generation, unless the GLOB option is unset. If the EXTENDED_GLOB option is set, the ‘^’ and ‘#’ characters also denote a pattern; otherwise they are not treated specially by the shell.

所以，解决方案就是通过加上noglob去取消通配符匹配

```sh
alias rake="noglob rake"
source ~/.zshrc
```