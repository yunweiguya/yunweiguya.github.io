---
layout: post
title: "sprint回顾"
date: 2014-07-08 16:57:32 +0800
comments: true
categories: [python]
---

### 1 

2014年06月24日 ~ 2014年07月04日，3个哥们一起组成兴趣小队折腾了下爬虫平台，算作1个sprint。涉及scrapy、tornado和py一些基础组件redis-py、pika、gearman、apscheduler、dbutils等。业务解决定时爬取、实时爬取、队列消费爬取，比较有意思的是vps服务模块。

兴趣是最好的老师，A君周末搞定py语法，然后研究scrapy，搞vps模块；B君果断扔掉sqlalchemy，写了个orm <= 之前我们用的torndb+dbutils。大家分享、交流很积极充分，难忘的协作经历~。web这块不喜欢twisted(scrapy基于这玩意)，用了tornado <= 后来扫尾玩了下flask，完备很多(当然没有异步io)，但仍感觉web范式不出rails。

### 2

py生态完备，写点后台小脚本挺不错的。现在前台web基本玩php，不写rails了~，不过gevent/eventmachine可以一起玩下。go暂时应该是没有场景用到。

### 3

后面打算写点java，研究netty和dubbo(<= 有了面包、空气和水plan基础理解上应该还好)，应对服务化。






