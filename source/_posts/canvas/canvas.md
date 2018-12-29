---
title: 玩玩canvas
tag: canvas
---
``` html
<canvas id="tutorial" width="300" height="300"></canvas>
```

1. canvas 在初始化宽高的时候建议不用css设置，如果设置的比例和初始的比例不同，则会造成扭曲，因此在开始的时候有两种写法：

1. 一种在标签直接加 `width`,`height`;
2. 一种是在获取完canvas标签节点后，在js给它加上宽高；
``` js
    let canvas = document.getElementById('canvas');
    if (!canvas.getContext) return;
    canvas.height = 100;
    canvas.width = 100;
```


## 绘制矩形

1. fillRect(x, y, width, height)
绘制一个填充的矩形

2. strokeRect(x, y, width, height)
绘制一个矩形的边框

3. clearRect(x, y, widh, height)
清除指定的矩形区域，然后这块区域会变的完全透明。

```js
    let ctx = canvas.getContext('2d');
    // 绘制填充矩形
    ctx.fillRect(10, 10, 100, 50);
    // 绘制矩形边框
    ctx.strokeRect(10, 70, 100, 50); 
    // 清除矩形
    ctx.clearRect(15, 15, 50, 25);
```

## 绘制路径

**在每次画完一条路径后就要closePath(),不然会影响下一个路径的绘制**
1. beginPath()
新建一条路径，路径一旦创建成功，图形绘制命令被指向到路径上生成路径

2. moveTo(x, y)
把画笔移动到指定的坐标(x, y)。相当于设置路径的起始点坐标。

3. closePath()
闭合路径之后，图形绘制命令又重新指向到上下文中

4. stroke()
通过线条来绘制图形轮廓

5. fill()
通过填充路径的内容区域生成实心的图形

## 绘制圆弧

1. arc(x, y, r, startAngle, endAngle, anticlockwise)
> x,y为坐标点，r为半径，startAngle，endAngle为角度，anticlockwise为绘制的方向，true为逆时针；