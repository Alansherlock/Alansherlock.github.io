---
title: blob 对象 对于二进制流生成本地地址的使用
tag: JavaScript
---


1. blob 对象在项目中最常用的则是在前端生成自己的地址，然后用于后端生成的图片或者文件，基本都是二进制格式的，哎，难受；

``` js

    let blob = new Blob(['后台给的字符串'],{type:'各种需要的格式'});//例如 image/jpg

    // 再利用生成地址的API
    let url = window.URL.windowCreateURL();//生成url则可以作用于当前页面

    //此刻，我需要来串通用的原生代码，因为，像jq封装的dataType:'blob'系不行滴，之前还写过一篇关于vue +axios的博文，也是用到了blob，如果有需要的也可以去看下
    // react 代码，不过不影响
    getImgCode() {
        let that = this;
        var xhr = new XMLHttpRequest();
        xhr.open("get", 'http://servicetest.changan.com.cn/changan-trade-application/api/v1/changan/trade/member/verify/code/image', true);
        xhr.responseType = "blob";
        xhr.setRequestHeader("openid", util.getLocalCache('openid'));
        xhr.onload = function () {
            if (this.status == 200) {
                var blob = this.response;
                that.setState({imgCode:window.URL.createObjectURL(blob)});
            }
        }
        xhr.send();
    }
```