---
layout:     post   				    # 使用的布局（不需要改）
title:      Weblogic ConSole HTTP 协议代码执行漏洞安全警告                # 标题
subtitle:                           #副标题
date:       2020-12-08 				# 时间
author:     DYD 				    # 作者
header-img: img/post-bg-debug.png 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 漏洞
    - vul
---

漏洞等级 High

CVE编号 CVE-2020-14882,CVE-2020-14883

漏洞详情Oracle发布2020年10月关键补丁更新，修复了多个评分为 9.8 的严重漏洞。其中Weblogic ConSole HTTP 协议代码执行漏洞 相关 POC已经公开，漏洞等级：严重。远程攻击者可以构造特殊的HTTP请求，在未经身份验证的情况下接管 WebLogic Server Console，并在 WebLogic Server Console 执行任意代码。

影响范围WebLogic 10.3.6.0.0
       WebLogic 12.1.3.0.0
       WebLogic 12.2.1.3.0
       WebLogic 12.2.1.4.0
       WebLogic 14.1.1.0.0

修复方案注意：安装升级前，请做好数据备份、快照和测试工作，防止发生意外

      1、升级官方安全补丁；

      2、使用WAF进行安全防御；

[参考链接](https://www.oracle.com/security-alerts/cpuoct2020traditional.html)

