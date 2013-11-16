---
comments: true
layout: post
title :  Javascript 折半搜索法（二分法）
categories : 
- Stack
tags : 
- JavaScript
---



周末，写个简单的算法。

JS二分法：
```javascript
Array.prototype.binarySearch = function (v) {

	var l = 0;
	var h = this.length - 1;

	while (l
<= h) {
		var m = l + ((h - l) >
	> 1);
		console.log('l@%s,h@%s,m@%s', l, h, m);
		if (this[m] === v) {
			return m;
		}
		if (this[m] > v) {
			h = m - 1;
		} else {
			l = m + 1;
		}
	}

	return -(l + 1);
}
```
使用：
```javascript
var arr = [1, 2, 3, 5, 78, 2312, 424];

arr.sort(function (x, y) {
	return x - y;
})
console.log(arr);
console.log(arr.binarySearch(424));
```
说明：

`var m = l + ((h - l) >> 1);`，为什么要用位运算？

其实用`var m = Math.floor((h+l)/2);`也是可以的，但是位运算的速度优于除法，并且还要再进行一次Math.floor。用位运算主要是出于性能考虑。`h+l`还存在溢出的问题，不过这个在web端应该不会遇到。。。Node.js就有可能了。

还有个复杂度的问题，下回再分析。


---
伊泽  
2013-07-29于杭州