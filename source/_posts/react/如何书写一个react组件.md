---
title: 书写一个react组件
tag: react
---
为什么要写react组件，react简单的组件改如何书写？

1. 在开始书写一个react组件的时候，我们需要了解到react的一些语法，这样才能在书写的过程中，不会有太多的疑问

> 就了解，当我书写一个react组件的时候，会有一系列的依赖的引入，最简单的莫过于一定要引入react，`import React,{Component} from React;`
> 这个是在写react哪个组件都要引入的react的依赖，紧接着，你可能还需要一些css也可以通过import的方式来引入到我们的组件当中，有一点需要注意的是，在引入的css样式中，我们需要用一个`根标签来包住`,防止在书写的时候被其他地方的样式污染；

2. react16的`<Fragment></Fragment>`

> 书写react，外围有时候需要用一个标签来包住，这个时候我们就可以像引入Component一样引入这个标签包裹在需要一个虚拟的div的地方，从而不会影响页面的布局
