---
title: react使用笔记
tag: react
---
对于react初步使用的总结

## react 使用

### react 中this指向问题

在使用react的时候，开始的时候因为this指向的问题用了bind，然而可以使用`e => {this.tabClick}`这种来让this的指向指向定义的那个类，减少代码量

### react中判断语句一般采用三元表达式来作判断

在react中，类似vue指令v-if的写法则是{true?use this: use this},这种来判断；

### react 中循环的写法

在循环上，则需要定义好map方法，`须记得return 出来当前书写完的这些`

### 获取地址栏参数

``` javascript
    this.props.location.query;// query则可以拿到一个对象，这个对象包含了传递的参数 【场景：mobx+react】
```

### react 导入HTML

``` html
    <div className='description'>
        <p dangerouslySetInnerHTML={{ __html: activityDetail.content }} />
    </div>
```

### react 虚拟标签(本人叫法，有点类似Vue里面经常使用的template标签)
``` jsx
    {x.imageUrl ?
    <Fragment>
        <img src={x.imageUrl} style={{ width: '90%' }} alt="图片查看" /><br />
    </Fragment> : null}
```