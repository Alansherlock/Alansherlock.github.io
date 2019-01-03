---
title: scrapy
tag: Python
---

## 安装scrapy

1. pip install scrapy (还可以用pip3)
2. 遇到pip版本过低的，跟着提示升级即可`python -m pip install --upgrade pip` 
3. pip install scrapy 
> 在第三步的时候，提示安装编译器`error: Microsoft Visual C++ 14.0 is required. Get it with "Microsoft Visual C++ Build Tools": http://landinghub.visualstudio.com/visual-cpp-build-tools`,还有这个`mysql-connector-python 8.0.13 requires protobuf>=3.0.0, which is not installed.`
A. **这个时候我们不需要去安装编译器，而是安装另外一个依赖包即可** [twisted相关包地址](https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted)，在twisted这一栏下载对应的依赖包到自己电脑，然后找到你下载好的文件路径，例如我的文件下载到了`D:\Python\Twisted-18.9.0-cp37-cp37m-win_amd64.whl`,在cmd继续运行 `pip install D:\Python\Twisted-18.9.0-cp37-cp37m-win_amd64.whl`,当最后报`Successfully installed Twisted-18.9.0`,即可进行安装scrapy，`pip install scrapy`,报`Successfully installed Scrapy-1.5.1`,即是安装成功；
B. mysql-connector-python 8.0.13这个则直接`pip install mysql-connector-python 8.0.13`即可

## scrapy解析

### 组件解析

1. `engine`,框架核心，其他组件在其控制下协同工作（内部组件）
2. `scheduler`,调度器，负责对spider提交的下载请求进行调度
3. `downloader`,下载器，负责下载页面（发送HTTP请求/接受HTTP响应）（内部组件）
4. `spider`,爬虫，负责提取页面中的数据，并产生对新页面的下载请求（用户实现）
5. `middleware`,中间件，负责对Request对象和Response对象进行处理（内容组件）
6. `item pipeline`,数据管道，负责对爬取到的数据进行处理（内部组件）

### 数据流

1. Request，scrapy的请求对象
2. Response，scrapy的响应对象
3. ITEM，从页面爬取的一项数据

### Request对象

一般情况下只有这两个参数，其他可选（method,headers,body,cookies,meta,encoding,priority = 0,dont_filter=False, errback）
priority,请求优先级,默认为0
``` python
yield scrapy.Request(url=next_url, callback=self.parse)
```

### Response对象

headers，这个可以通过get方法进行访问里面的数据，
``` python
response.headers.get('Content-Type')
response.headers.get('Set-Cookie')
```

### Selector对象

可以供使用的有Xpath和css两种语法的代码，
``` python
# 选择文档中的h1标签，有多个则拼成数组
selector_list = selector.xpath('//h1')
```

使用这个对象提取数据的方法有`extract_first(),re_first()`,前提是数组哈，不是数组的用另外的这两个`extract(),re()`
re这种写法是搞正则匹配的，`re_first('\d+\.\d+')`,提取小数点左右的数字；

###XPath




