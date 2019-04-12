---
title: github被屏蔽后如何提交代码
tag: github
---
往github上提交代码一直提示错误信息“fatal: unable to access 'https://github.com/xxxx.git/': Failed to connect to github.com port 443: Connection refused“，被墙了，需要使用代理。

## github代理配置

``` js
    // 1080为我自己VPN本地代理启用的端口号，可替代为自己VPN的端口号
    git config --global http.proxy "localhost:1080"
```

执行完楼上的命令后，即可`git push`,心情愉悦！！！
