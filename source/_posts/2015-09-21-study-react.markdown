---
layout: post
title: "Study React"
date: 2015-09-21T00:41:36+08:00
tags:
 - study
 - react
---

# React 学习笔记

> A JAVASCRIPT LIBRARY FOR BUILDING USER INTERFACES

引言是 [React 官网](http://facebook.github.io/react/) 上是的自述。React 主要是用于构建用户界面。

## 为什么使用 React?

React 是一个 Facebook 和 Instagram 用来创建用户界面的 JavaScript 库。主要采用以下两个思想：

- 简单

	仅仅只要表达出你的应用程序在任一个时间点应该长的样子，然后当底层的数据变了，React 会自动处理所有用户界面的更新。

- 声明式

	 数据变化后，React 概念上与点击“刷新”按钮类似，但仅会更新变化的部分。


## 几个特点

- 仅仅是 UI

	许多人使用 React 作为 MVC 架构的 V 层。尽管 React 并没有假设过你的其他技术栈，但你仍可以作为一个小特征轻易地在已有项目中使用。

- 虚拟 DOM

	React为了更高超的性能而使用虚拟DOM作为其不同的实现。 它同时也可以由服务端Node.js渲染 － 而不需要过重的浏览器DOM支持。

- 数据流

	React实现了单向响应的数据流，从而减少了重复代码，这也是它为什么比传统数据绑定更简单。

## 几个概念

-  React elements

	`React 元素（React elements）` 是一些用于表示 HTML 元素的 JavaScript 对象，他们并不存在于浏览器中，浏览器原生对象在 React 中，也有对应的 React 元素对应，比如 `h1` 、 `div` 、`section`。


- Components

	`组件（Components）`也就是我们常说的组件，他们一般是构成我们页面的最大的一部分，主要包括「结构」和「功能」。举个例子，比如 `NavBar` 、 `LikeButton` 、`ImageUploader` 都是一个个带有结构和功能的组件。

	组件就像是函数。接受`props`和`state`作为参数，渲染出`HTML`。

- JSX

	`JSX` 是一个看起来想 XML 的 JavaScript 语法扩展。举个例子：`<h1>Hello</h1>` 是 `React Element` 使用 `JSX` 的语法的写法。同样的，如果你不用 `JSX` ，使用这样的写法：`React.DOM.h1(null, 'Hello')` 也可以达到相同的效果。相比之下 `JSX` 的易读性更好。 JSX 需要编译之后才能在浏览器中运行。`JSX`并不是强制使用的，这个语法只是让搭建 React 应用变得更加地简单。

- The Virtual DOM

	`虚拟 DOM（The Virtual DOM）`  是存在于内存之中的一种数据结构，并不是真正的 DOM 节点。只有当他插入到文档中以后，才会变成真正的 DOM 。React 会监听虚拟 DOM 的变化，会自动的计算 DOM 和 虚拟 DOM 的区别。所有 DOM 的变动，都会先在 虚拟 DOM 上发生，然后再将实际变动的部分，反应在真实的 DOM 上，这种算法叫 DOM diff ，它极大的提高了网页性能表现。

需要先稍微理解下以上的几个概念，方便

## 渲染

我们首先来看下怎么把 虚拟 DOM （React 元素和组件都是虚拟 DOM）渲染到页面上。我们知道，虚拟 DOM 只存在于内存中，我们需要告诉 React ，以让它执行虚拟 DOM 的渲染。

``` javascript
React.render(<h1>Hello World</h1>, document.getElementById('app'));
```

上面的代码会将一个 H1 ，插入到 body 上。

`render` 函数接收两个参数，第一个参数为 `React element`，第二个参数为 `DOM element`。

## 组件

组件是 React 的重要组成部分，是自定义的 React 元素。一个组件就是一个功能。

``` javascript
var HelloWorld = React.createClass({
	render: fucntion(){
		return (<h1>Hello World!</h1>)
	}
})

React.render(<HelloWorld />, document.getElementById('app'));
```


`createClass` 方法的参数是个对象，这个对象需要包含 `render`函数。

在上段代码中，通过 `createClass` 我们创建了 `HelloWorld` 元素，然后我们通过 `React.render` 方法将 `HelloWorld` 元素渲染到了 `#app` 里面。

这个例子和上一个差不多，区别是你可以为 `HelloWorld` 元素添加更多的自定义方法和逻辑了。

> 注意 自定义的 React 元素，第一个字母需要大写。


##  Props

`Props` 我们可以理解为组件的参数。通过 `HTML` 的属性传入。

``` javascript
var HelloWorld = React.createClass({
	render: fucntion(){
		return (<h1>Hello World! {this.props.author}</h1>)
	}
})

React.render(<HelloWorld author='somebody'/>, document.getElementById('app'));
```

在 `React.render` 方法中，我们传入了 `author` 这个参数。这个参数在 `HelloWorld` 组件的 `render` 通过 `this.props.author` 取得。

所有通过 `ReactElement` 传入的参数，都可以在组件的 `render` 方法中获取到。值得注意的是，`ReactElement` 是通过 `JavaScript` 创建的，`class` `for` 等均为 `JavaScript` 的保留字，在 `JSX` 中不能直接写 `class` 和 `for`，而需要写成 `className` 和 `htmlFor`：

``` javascript
React.render(<label htmlFor="inputEl"><input type="text" className="input-el" id="inputEl"/></label>)
```

### this.props.children

this.props 对象的属性和组件的属性一一对应，但是有一个是例外的， 就是 `this.props.children` 。它表示的是组件的所有子节点。

``` javascript
var List = React.createClass({
  render: function() {
    return (
      <ul>
      {
        this.props.children.map(function (child) {
          return <li>{child}</li>
        })
      }
      </ol>
    );
  }
});

React.render(<list><span>Hello</span><span>World</span></list>)
```

> 注意：你没有办法通过 `this.props.children` 取得当前组件的子元素，因为 `this.props.children` 返回的是组件传递给你的 `Passed onto you` 子节点。




