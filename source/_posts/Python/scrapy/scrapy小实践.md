---
title: scrapy
tag: Python
---
搞起来，scrapy
1. 安装完scrapy后，开始初始化项目
``` python
    # 初始化项目名为example
    scrapy startobject example
```

2. 直接开始书写爬虫的Spider文件，在spiders中建立book_spider.py,书写以下代码来抓取全书网的某页的书籍名称和书籍作者，然后保存一个csv文件
``` python
# 引入框架
import scrapy
class BooksSpider(scrapy.Spider):
    #爬虫唯一名称
    name = 'books'
    # 爬取的网页，可爬取多个
    start_urls = ['http://www.quanshuwang.com/list/1_1.html']
    # 定义对爬取响应回来的内容做处理
    def parse(self,response):
        # 爬取的是当前这个列表，需要定义的css从根节点开始，即 li标签
        for book in response.css('.seeWell.cf li'):
            # xpath 语法
            name = book.xpath('./span/a/@title').extract_first()
            # css语法
            author = book.css('span a:nth-child(2)::text').extract_first()
            # 处理返回 name和author
            yield {
                'name':name,
                'author':author
            }
```

3. 执行`scrapy crawl books -o books.csv`,即可生成对应的books.csv文件
4.其他的内容下次继续。。。