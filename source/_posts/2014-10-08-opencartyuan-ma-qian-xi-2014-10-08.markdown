---
layout: post
title: "OpenCart源码浅析2014-10-08"
date: 2014-10-08 22:38:55 +0800
comments: true
categories: 
---
# 更新log
	1. 2014-10-08 index.php
	
# 初衷
	想看看社区迭代过的商城各模块是如何设计的，并给团队做分享。
# upload/index.php
##### upload/system/startup.php 主要做两件事情：
	1. spl_autoload_register('autoload'); 来加载library/下的类。
	2. 加载Engine(action、controller、event、front、loader、model、registry)和Helper。

##### Engine
	1. Registry 注册表模式，全局k-v数组。
	2. Action 根据$route找到文件，通过call_user_func_array调用upload/catalog/controller/下相应controller的action。
	3. Loader 手动加载model、view、library、helper。
	4. Event 保留一堆Actions来trigger。
	5. Front dispatch分发器。addPreAction添加前置处理。dispatch链式执行。

##### Config 全局配置array
	利用autoload加载library/config.php类，存setting表中k-v。

##### 其它
	1. error_handler和超简单Log。
	2. Request，递归参数过滤一堆php变量:$_GET $_POST $_REQUEST $_COOKIE $_FILES $_SERVER。
	3. Response，HTTP头操作，《HTTP权威》要再细看。
	4. Cache分为APC、File、Memcache 3种，文件实现简单干净。
	5. language表匹配HTTP头语言。
	6. tracking参数更新marketing表中clicks。
	7. Encryption 加密工具类。
	
	
##### Document

# 业务实体
	全部db操作、表大量text字段应对较大流量值得商榷。
##### Customer

##### Affiliate 联盟营销Affiliate Marketing

##### Cart 购物车*****

##### Tax

##### Product 商品 ******

##### Category 类目 ******

##### Coupon 促销 ******

##### Voucher 礼品劵 ***

##### Order 订单 ******








##### 度量单位
	1. Currency和currency表
	2. Weight和 weight_class、weight_class_description表
	3. Length
	
### TODO
	1.redis cache加入(Predis)。
	2. ...

	

	
