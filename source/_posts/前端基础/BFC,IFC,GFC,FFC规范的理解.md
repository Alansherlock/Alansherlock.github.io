---
title: BFC,IFC,GFC,FFC规范的理解
tag: 前端基础
---

BFC (Block Formatting Context )指块级格式化上下文，即一个创建了新的BFC的盒子是独立布局的，盒子里面的子元素的样式不会影响到外面的元素 。
在同一个BFC中，两个毗邻的块级 盒在垂直方向(和布局方向有关系 )的margin会发生折叠 。BFC 决定元素如何对其内容进行布局，也决定与其他元素的关系和相王作用 。

IFC ( Inline Formatting Context )指内联格式化上下文 。 IFC 的线柜( line box )
高度由其包含行内元素中最高的实际高度计算而来(不受竖直方向的 padding/margin 的 影响)。 IFC 中的线框一般左右都贴紧整个 IFC，但是会被 float 元素扰乱 。 同一个 IFC 下 的多个线柜高度不同 。 IFC 中是不可能有块级元素的，当插入块级元素时(如在 p 中插入 div )，会产生两个匿名块，两者 与 div 分隔开，即产生两个 IFC， 每个 IFC 对外表现为块级 元素，与 div 垂直排列 。

GFC ( GridLayout Formatting Context )指网格布局格式化上下文，即当把一个
元素的 display 值设为 grid 的时候 ，此元素将会获得 一 个独立的渲染区域 。 可以通过在 网格容器( grid container )上定义网格定义行( grid definition row )和网格定义列( grid definition column )，在网格项目( grid item ) 上 定义网格行( grid row )和网格列( grid
column )来为每一个网格项目定义位 置和空 间 。

FFC (FlexFormattingContext)指自适应格式化上下文，即 display值为 flex或 inline-flex 的元素 将会生成自适应容器。伸缩容器中的每 一 个子元素都是 一 个伸缩单元 。 伸缩单元可以是任意数量的 。 伸缩羊元内和伸缩容器外的 一切元素都不受影响 。 简单地 说， Flexbox 定义了伸缩容器内伸缩单元的布局。
