---
title: react基础知识
tag: react
---

## 更新数据的this.setState()

在日常使用中，都是直接就this.setState()，里面包裹着一个对象然后直接的更新好数据例如：
``` javaScript
    this.setState({isTrue:true});
```

然后，在一些场景中，由于数据量大，保存的时候会因为没存储完就立马去调用下一步操作，这个时候，我也尝试了 `async + await`,ES7中异步的操作，但是还是没啥变化，最后在查阅资料的过程中，发现`this.setState()`还可以有函数的参数，例如：
``` javaScript
    this.setState({isTrue:true},()=> {
        // 在这里做一些存储完数据后的操作
    });
```
在react后续的版本中，setState方法还可以是函数的形式，例如：
``` javaScript
    this.setState(
        // 这样也能达到更新值的目的，两个参数，在一些异步的场景说会用到
        (prevState, props) => (
            { count: prevState.count + 1 }
        )
    );
```

## {true?true:false}(三元表达式) || && 

``` javaScript
    /*
     三元表达式
     比较了vue 和 react的函数式三元判断，还是觉得Vue的舒服些
    **/
    {isLoading ? <div className="empty">数据加载中...</div> : ""}
    /*
    或字符 || 
    好像这个在HTML中少用到，数据上倒是经常
    **/
    {activityLists == null ||
        activityLists.length == 0 && 
        <div className="empty">暂无活动~</div>
    }
    /*
    &&在看了人家的代码才知道这个也可以搞起来，没必要天天用三元运算符
    **/
    {activityList.total > 10 && loadEnd && (
        <div className="empty">数据加载完毕</div>
    )}
```

## 跳转路由的方式

在日常的框架中，都有一个是直接就跳转能够存储到，还有一个replace直接不能后退，如下写法：

``` javaScript
    this.props.router.push
    this.props.router.replace
    // 在使用的过程中，可以在入口中直接定义好，可以简短些书写，如下：
    componentWillMount() {
        window.app = {
            goto: this.props.router.push,
            replace: this.props.router.replace
        };
    }
    // 在其他地方的写法，则可以直接是如下：
    window.app.goto('login');
    window.app.replace('login');
```

## 路由的写法

在接触的移动端中，路由用的4，写法感觉和之前Vue的路由大同小异，如下：

在引入入口的render中就开始书写上router,如下：
```javaScript
    // Stores 和 Routes 的初始化
    // 使用React-Router 3 效果会更好
    import { Router, hashHistory } from "react-router";
    // 导入Provider
    import { Provider } from "mobx-react";
    const rootEl = document.getElementById("root");
    render(
        <Provider {...Stores}>
            <Router history={hashHistory} routes={routes} />
        </Provider>,
        rootEl
    );
```
接下来则是引入路由的路径
``` javaScript
    import App from "./App";
import { uservistIng } from './biz/home/index/userVistIngServ'
function setTitle(title) {
  window.document.title = title;
}
// 进入路由之前的处理，检查是否已登录
const beforeEnter = async (nextState, replace, next) => {
  await uservisits();
  next()
}
async function uservisits() {
  await uservistIng();
}
export default [
  {
    path: "/",
    component: App,
    indexRoute: { onEnter: (nextState, replace) => replace("/home") },
    childRoutes: [
      {
        path: "home",
        getComponent: (nextState, cb) => {
          setTitle("长安汽车尊享服务");
          import("biz/home/index/IndexView").then(x => {
            cb(null, x.default);
          });
        },
        onEnter: beforeEnter
      },
      {
        path: "chat",
        title: "VIP服务室",
        getComponent: (nextState, cb) => {
          import("biz/home/chat/IndexView").then(x => {
            cb(null, x.default);
          });
        },
        onEnter: beforeEnter
      }
    ]
  }
```






