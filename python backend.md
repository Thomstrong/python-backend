# Python 后端复习资料

- ## Tornado

  - Python 语言写成的 Web服务器兼Web应用框架

  - 性能对比

    ![Python Web 框架](D:\Thomstrong\复习资料\review-for-job\python Web框架性能对比.png)

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

- ## 数据库相关

  - 性能对比

    ![数据库性能对比](D:\Thomstrong\复习资料\review-for-job\数据库性能对比.jpg)

  - 分类

    - 关系型数据库：SQL Server、Oracle、MySQL、 PostgreSQL、DB2...
      - 支持关系（基于表的 ）数据模型，每条数据都有固定的属性及对应值，即对于同一个表的每条数据需要有相同的属性
        - 关系：可理解为表
        - 元组：表中的一行
        - 属性：表中的一列
        - 域：属性的取值范围（类型）
        - 关键字：主键
      - 优点：易理解、方便使用、易于维护
      - 瓶颈：高并发读写需求、海量数据的高效率读写、高扩展性和可用性、
      - Web不需要的特性：事务一致性、读写实时性、复杂SQL尤其是多表关联
      - ACID：Atomic、Consistency、Isolation、Durability
    - 非关系型数据库：MongoDB、Redis、CouchDB
      - NoSQL：用于指代那些非关系型的，分布式的，且一般不保证遵循ACID原则的数据存储系统
      - Key-Value存储模式，每个元组可以根据需要 增加自己的KV对，结构不固定，较少时间和空间的开销。用户可根基需要自己添加需要的字段。仅需根据id即可取出相应的value。
      - 由于较少的约束，没有类似SQL一样的where查询，难以体现设计的完整性，适合存储较为简单的数据，对于需要复杂查询的数据使用SQL更为合适
      - 分类：
        - 面向高性能并发读写的k-v数据库:Redis
        - 面向海量数据访问的文档数据库:MongoDB
        - 面向可扩展性的分布式数据库

- ## Linux相关

  - SSH (secure shell)
    - 功能：实现字符界面的远程登录，SSH协议对通信双方的数据传输进行了加密处理，需对远程访问的用户进行口令登录
    - 端口：22
    - 协议：SSH V2协议
    - 验证方式：
      - 密码验证：以服务器中本地系统用户的登录名称、密码进行验证
      - 密钥对验证：提供相匹配的秘钥信息才能通过验证，通常先在客户机中创建一对迷药文件（公钥和私钥）然后将公钥放到服务器中的指定位置
    - 登录方式：ssh username@ip

- ## Python

  - 综述
    - 解释型语言，无需编译
    - 动态类型语言，声明变量时无需说明变量类型
    - 非常适合面向对象编程，支持通过组合和继承的方式定义类，且没有访问说明符（private/public）
    - 函数即可被指定给特定变量，作为函数的输入，也可接受函数的返回值
    - 编写快但运行速度比编译型语言慢，但是提供了扩展接口
    - 用途广泛，可以作为其他语言或组件的“胶水语言”
    - KISS原则（Keep It Simple andStupid）
  - 多线程
    - Python并不支持真正意义上的多线程，提供了多线程包，但如果想通过多线程提高代码的速度，使用多线程包并不是好主意。
    - Python中有一个Global Interpreter Lock（GIL），确保任何时候你的多个线程中只有一个被执行，由于线程的执行速度非常快，会让人误以为是并行执行线程的，且经过GIL会增加执行开销
    - 在不考虑效率问题时，使用这个包完全没有问题；但是大多数情况是将多线程的任务交给操作系统（multiprocessing 创建多进程）、交给外部程序（Hadoop、Spark）或者调用其他代码（Python中的C函数）
  - 知识点
    - 函数默认参数若为可变参数则共用地址
    - 不确定函数的传入参数个数时使用fun(*args, **kwargs)
      - args以普通参数形式传入，传入后以元组形式呈现
      - kwargs以指定参数名方式传入，传入后以字典形式呈现

- ## GitHub

  - 简介
    - 版本控制


