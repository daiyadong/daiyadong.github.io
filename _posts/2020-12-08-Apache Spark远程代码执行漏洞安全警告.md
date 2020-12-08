---
layout:     post   				    # 使用的布局（不需要改）
title:      Apache Spark远程代码执行漏洞安全警告                # 标题
subtitle:                           #副标题
date:       2020-12-08 				# 时间
author:     DYD 				    # 作者
header-img: img/post-bg-debug.png 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 漏洞
    - vul
---


漏洞等级  High

CVE编号  CVE-2020-9480

漏洞详情

Apache Spark的独立资源管理器的主服务器可以通过配置共享密钥进行认证（spark.authenticate），但是在认证启用之后，即使没有共享密钥，也可以通过发送到主服务器的精心构造的远程过程调用指令在Spark集群上成功启动应用程序的资源，攻击者可以利用该漏洞在主机上执行任意命令。

影响范围

Apache Spark < = 2.4.5

修复方案

注：升级更新前请做好数据备份、快照和测试工作，防止发生意外
1.Spark 更新到2.4.6或3.0.0以上版本

[参考链接](http://spark.apache.org/security.html)

[参考链接2](
https://github.com/apache/spark/releases)
