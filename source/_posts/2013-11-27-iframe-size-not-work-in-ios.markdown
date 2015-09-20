---
layout: post
title: "iframe-size-not-work-in-IOS"
date: 2013-11-27 10:02
comments: true
categories: 
- Stack
tags:
- IOS
- CSS
---

最近遇到一个问题，就是iFrame在iPad上展示的时候，宽度并没有固定，会直接超出，通过嵌套div之后，无法滚动。

HTML
```html
<div class="frame_holder">
  <iframe class="my_frame">
    // The content
  </iframe>
</div>
```

CSS
```css
body {
  position: relative;
  background: #f0f0f0;
}

.frame_holder {
  position: absolute;
  top: 50px;
  bottom: 50px;
  left: 50px;
  right: 50px;
  background: #ffffff;
}

.my_frame {
  width: 100%;
  height: 100%;
  border: 1px solid #e0e0e0;
}
```

例子：

[http://jsfiddle.net/R3PKB/2/](http://jsfiddle.net/R3PKB/2/)

可以在你的iPad上去看看这个页面

[http://jsfiddle.net/R3PKB/2/embedded/result](http://jsfiddle.net/R3PKB/2/embedded/result)

解决方案是：

在外层的`div`上添加`overflow:auto`和`-webkit-overflow-scrolling:touch`就可以了。

[http://jsfiddle.net/R3PKB/7/](http://jsfiddle.net/R3PKB/7/)

参考链接：

- [http://stackoverflow.com/questions/16937070/iframe-size-with-css-on-ios](http://stackoverflow.com/questions/16937070/iframe-size-with-css-on-ios)

- [http://stackoverflow.com/questions/6139564/iframe-size-on-ipad/6721310#6721310](http://stackoverflow.com/questions/6139564/iframe-size-on-ipad/6721310#6721310)

- [http://stackoverflow.com/questions/9814256/iframe-on-ios-ipad-content-cropping-issue](http://stackoverflow.com/questions/9814256/iframe-on-ios-ipad-content-cropping-issue)