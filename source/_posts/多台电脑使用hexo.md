---
title: 解决多台电脑使用hexo的问题
tag: hexo
---
在使用hexo的过程中，我开始是在上家公司写的东西全部提交到了hexo，以为就好了，结果换新公司从新电脑拉下来后不知道怎么搞了，原先的那些东西都没了，为了解决这个，我在度娘上找到了方案，写在这里，做下记录
![](http://phcp7w60f.bkt.clouddn.com/7c96498fee2dace1c961c1fd3a5a410b.gif)


## 解决方案

1. 在线上的git仓库上新建一个分支，例如名字为hexo;

![](http://phcp7w60f.bkt.clouddn.com/hexo1.jpg)

2. 在当前的仓库的Settings > Branchs 更新hexo分支为默认分支 

![](http://phcp7w60f.bkt.clouddn.com/hexo2.jpg) 

3. 更新完后我们将代码都拉取下来，拉取的是hexo分支了现在，此时我们看到的东西是长这样的

![](http://phcp7w60f.bkt.clouddn.com/hexo3.jpg)

4. 此时，我们开始下一步操作，我们将本地之前hexo搞的那整一份全部拷贝进入我们的这个hexo（谨记，将themes里面的.git先删除），接下来我们看到的文件夹是这样的

![](http://phcp7w60f.bkt.clouddn.com/hexo4.jpg)

5. 此时我们可以运行一些命令把这一份代码提交到GitHub了，`git add .` `git commit -m 'some description'` `git push`,这样到线上看到的就已经把整一个静态资源的也push上去了，在线上看到如下，

![](http://phcp7w60f.bkt.clouddn.com/hexo5.jpg)

6. 此时，我们已经算完成了，接下来我们再到另外一台电脑来试试， 搞好ssh,然后克隆到新电脑，紧接着我们`npm i `,安装一些依赖，书写完文件后，执行hexo d -g指令（在此之前，有时可能需要执行hexo clean），完成后就会发现，最新改动已经更新到master分支了，两个分支互不干扰！



> 有问题可以联系我邮箱 `Alansherlock@163,com`,或者留言评论！哈哈哈
