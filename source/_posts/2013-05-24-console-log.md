---
comments: true
layout: post
title : console.log
categories : 
- Stack
tags : 
- Browser
---


作为开发人员，用好调试工具可以提高工作效率，今天就来说说`console.log`

`console.log` 很简单，

```javascript
	console.log(1)
	console.log($0) //$0是elements panel 里面你选中的DOM结构。也可以使用console.dir($0)
	console.log(1,2) //多参数 
```
以上这些都是基本的用法，不赘述。

下面就来说说，你可能不知道的console.log

```javascript
	var userName = "yize",userPoints = 100;
	console.log("User %s has %d points", userName, userPoints);
```
运行以上命令，控制台会输出User yize has 100 points

$s,$d看起来是不是特别眼熟，貌似是大学的时候学过的C语言，哈哈

chrome dev tools 目前支持以下几种格式：
<table>
	<thead>
		<tr>
			<th>Format Specifier</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>
				<code>%s</code>
			</td>
			<td>Formats the value as a string.//字符串</td>
		</tr>
		<tr>
			<td>
				<code>%d</code>
				or
				<code>%i</code>
			</td>
			<td>Formats the value as an integer.//整形</td>
		</tr>
		<tr>
			<td>
				<code>%f</code>
			</td>
			<td>Formats the value as a floating point value.//浮点数</td>
		</tr>
		<tr>
			<td>
				<code>%o</code>
			</td>
			<td>
				Formats the value as an expandable DOM element (as in the Elements panel).//DOM元素
			</td>
		</tr>
		<tr>
			<td>
				<code>%O</code>
			</td>
			<td>Formats the value as an expandable JavaScript object.//JS对象</td>
		</tr>
		<tr>
			<td>
				<code>%c</code>
			</td>
			<td>
				Formats the output string according to CSS styles you provide.//CSS 样式
			</td>
		</tr>
	</tbody>
</table>
目测`console.log('%O',document.body) === console.dir(document.body)`

改变log的样式：

```javascript
	var userName = "yize",userPoints = 100;
	console.log("%cUser %s has %d points", "color:orange; background:blue; font-size: 16pt", userName, userPoints);
```
![图片](http://ww3.sinaimg.cn/large/60ee1ef8gw1e4z9k9snadj218i03e75p.jpg)
chrome dev tools很强大，官方文档:[https://developers.google.com/chrome-developer-tools/]()

---
伊泽  
2013-5-24于杭州