---
title: git不同账号同一台电脑的配置
tag: git
---
在多次谷歌和百度后，终于在尝试中试出了方案，如下：

## window中的配置

### 文件的位置

.git 存在于项目中
.ssh 则是在C盘的用户路径下
ssh_config存在于C盘Program Files中的Git/etc/ssh

``` js
Host gogs.dtyunxi.cn
        HostName gogs.dtyunxi.cn
        PreferredAuthentications publickey
        IdentityFile ~/.ssh/id_rsa.github
        IdentitiesOnly yes
        User liu.zehao
Host second.gogs.dtyunxi.cn
        HostName gogs.dtyunxi.cn
        PreferredAuthentications publickey
        IdentityFile ~/.ssh/id_rsa.changanan
        IdentitiesOnly yes
        User Alan
```

> Host 中配置的是当前类似于GitHub或者Gitlab或者码云的一个地址，关键在于`User`,以及`IdentityFile`，需要分别的对应到你的项目中，我们可以看到Host是不一样的，这个会在下一步起效果，即是配置到项目中的.git文件夹中的config文件

``` 
[core]
	repositoryformatversion = 0
	filemode = false
	bare = false
	logallrefupdates = true
	symlinks = false
	ignorecase = true
[remote "origin"]
	url = ssh://git@second.gogs.dtyunxi.cn:10022/changan/changan-b2c-web-h5.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
	remote = origin
	merge = refs/heads/master
[branch "dev"]
	remote = origin
	merge = refs/heads/dev
[branch "alan"]
	remote = origin
	merge = refs/heads/alan
[branch "test"]
	remote = origin
	merge = refs/heads/test
[user]
	name = alan
	email = alansherlock@163.com
```
> 可以明显的看到origin这里的ssh地址发生了更改对应到了楼上所配置的Host地址，这样就算大功告成了
``` 
[remote "origin"]
	url = ssh://git@second.gogs.dtyunxi.cn:10022/changan/changan-b2c-web-h5.git
	fetch = +refs/heads/*:refs/remotes/origin/*
```

### Mac中的配置

