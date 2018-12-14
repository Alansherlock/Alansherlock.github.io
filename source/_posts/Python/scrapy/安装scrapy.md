---
title: 安装scrapy
tag: python
---

1. pip install scrapy (还可以用pip3)
2. 遇到pip版本过低的，跟着提示升级即可`python -m pip install --upgrade pip` 
3. pip install scrapy 
> 在第三步的时候，提示安装编译器`error: Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual C++ Build Tools": http://landinghub.visualstudio.com/visual-cpp-build-tools`,还有这个`mysql-connector-python 8.0.13 requires protobuf>=3.0.0, which is not installed.`
A. **这个时候我们不需要去安装编译器，而是安装另外一个依赖包即可** [twisted相关包地址](https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted)，在twisted这一栏下载对应的依赖包到自己电脑，然后找到你下载好的文件路径，例如我的文件下载到了`D:\Python\Twisted-18.9.0-cp37-cp37m-win_amd64.whl`,在cmd继续运行 `pip install D:\Python\Twisted-18.9.0-cp37-cp37m-win_amd64.whl`,当最后报`Successfully installed Twisted-18.9.0`,即可进行安装scrapy，`pip install scrapy`,报`Successfully installed Scrapy-1.5.1`,即是安装成功；
B. mysql-connector-python 8.0.13这个则直接`pip install mysql-connector-python 8.0.13`即可
