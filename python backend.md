# Python 后端复习资料

- ## Tornado

  - Python 语言写成的 Web服务器兼Web应用框架

  - 性能对比

    ![Python Web 框架](D:\Thomstrong\复习资料\python Web框架性能对比.png)

- ## Django

  - Python 开源Web应用框架，使用MVT软件设计模式
    - 包括面向对象的映射器，用作数据模型（model.py）和关系型数据库间的媒介
    - 基于正则表达式的URL分发器(urls.py)，前端URL与后端请求函数相对应
    - 视图系统，处理请求(views.py)，后端的主要处理函数
    - 模板系统(template)
  - 数据库支持：PostgreSQL、MySQL、SQLite、Oracle

- ## Scrapy

  - 爬取网站数据，提取结构性数据而编写的应用框架
  - 架构组件包括
    - Scrapy Engine——控制数据流在系统中所有组件中流动，并在相应动作发生时触发事件。
    - Scheduler——调度从引擎接受的request并将他们入队，以便之后引擎请求他们时提供给引擎
    - Downloader——负责获取数据并提供给引擎
    - Spider——主要编写部分，分析response并提取item或额外跟进的URL的类。每个Spider负责处理一个或一些特定的网站
    - Item Pipeline——处理被Spider提取出来的item，如清理、验证、持久化等等
    - middewares
      - Downloader middlewares——在引擎及下载器之间的特定钩子，处理Downloader传递给引擎的response，可以通过插入自定义代码来扩展Scrapy功能，例如实现爬虫自动更换UA、IP等功能
      - Spider middlewares——引擎及Spider之间的特定钩子，处理spider的输入（response）和输出（items及requests）
  - 数据流
    1. 打开第一个网站，找到处理该网站的Spider并向该Spider请求第一个要爬取的URL
    2. 引擎从Spider中获取第一个要爬取的URL并在Scheduler以Requests调度
    3. 引擎向Scheduler请求下一个要爬取的URL
    4. Scheduler返回下一个要爬取的URL给引擎，引擎将URL以requests通过Download middlewares转发给下载器
    5. 网页下载完毕下载器生成一个该页面的Response，并将其通过Download middlewares发送给引擎
    6. 引擎从Downloader中接收到response 并通过Spider middlewares 发送给Spider处理
    7. Spider处理Response并返回爬取到的Item及新的Request给引擎
    8. 引擎将爬取到的item给item pipeline 并将Request给调度器
    9. 重复第二步直到调度器中没有更多的Request，引擎关闭该网站
  - 优势
    - 成熟的爬虫框架，有健全的管理系统
    - 分布式爬虫，高效
  - Selector——XPath语法 response.xpath('xpath表达式').extract()
    - / 从根节点选取节点
    - // 无视位置选取节点
    - . 当前节点
    - .. 父节点
    - @ 选取属性
    - [] 选定位置
      1. [n] 第n个元素
      2. [cotains(属性，值)] 选取某属性为某值的节点

