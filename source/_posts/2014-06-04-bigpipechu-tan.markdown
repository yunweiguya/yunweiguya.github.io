---
layout: post
title: "BigPipe初探"
date: 2014-06-04 22:19:24 +0800
comments: true
categories: [php]
---


	bigpipe在facebook应用是2010.6的事了，应用场景主要是个人首页，链接地址是:
	
	https://www.facebook.com/notes/facebook-engineering/bigpipe-pipelining-web-pages-for-high-performance/389414033919
	
	很有意思的是，bigpipe这种行事方式并没有铺广开来，微博的应用在2011年，场景也主要是个人相关页面。主要应该是seo的考虑，bigpipe这种略微激进的SJR(Server-generated JavaScript Responses)方式对seo是毁灭性打击(当然,可以检查是否是Bot,然后分开做)，同样，禁用js同样不能采用bigpipe，只能切回渲染...
	
	bigpipe可以理解成AJAX模块化方式的性能加强版(当然http请求会减少)，最主要的目的是利用流水线思想降低网页的用户感知延迟。
	
	在php侧做bigpipe这件事情，要并行去组织Pagelets，用多进程(pcntl)可以么? 我们知道现有ZTask 和 ZTaskManager都是跑完拉倒，结果怎么拿回来? 除了中转方式外，好像只能通过IPC. 于是重新翻了下APUE(《UNIX环境高级编程》), Linux 下进程间通信 (IPC) 的方式数很多:pipe、FIFO、POSIX 消息队列、共享内存、信号 (signals)、Sockets;同步原语有互斥器 (mutex)、条件变量 (condition variable)、读写锁 (reader-writer lock)、文件锁 (Record locking)、信号量 (Semaphore) 等等。明显只有Sockets简单靠谱，其他IPC都不能跨机器，而且本机多进程(多线程)是不利于模块化的，如果把pagelet流水线工厂抽出去...
	
	我们需要的其实只是异步IO +事件回调的机制来生成pagelets,这事java有future, php呢？ 只有yar了...
	
	咨询了下，某公司现在是用@laruence的yar，据说，pagelet后端并行化坑略多... 服务器的负载是增加的，整体传输时间不会减。bigepipe最的好处应该是模块化了所有区块。
	
	如果要通过优化把负载降下来，ESI应该有用。
		
	最后，从实现上来说，Bigpipe是一个需要RIA和Server端全力配合的技术。所以，在请教@华黎的时候，他直接让我去找@玉伯了...
	
	bigpipe的应用场景、大致方式应该是这样子了，个人感觉场景略少，对现有业务方式侵入还是比较大的，投入产出比相对来讲并不高。