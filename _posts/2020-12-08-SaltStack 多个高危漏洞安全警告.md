---
layout:     post   				    # 使用的布局（不需要改）
title:      SaltStack 多个高危漏洞安全警告                # 标题
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

CVE编号 CVE-2020-16846、CVE-2020-17490、CVE-2020-25592

漏洞详情

SaltStack官方发布安全更新，修复了多个漏洞。
CVE-2020-16846：可通过网络访问Salt API的未经身份验证的用户，可使用Shell注入，通过SSH客户端在Salt-API上运行代码。
CVE-2020-17490:Salttls执行模块 中函数 create_ca ， create_csr 和 create_self_signed_cert 中存在逻辑漏洞，不能确保密钥使用正确的权限创建。本地攻击者通过以低权限用户登录 salt 主机，可以从当前 salt 程序主机上读取到密钥内容，导致信息泄漏。
CVE-2020-25592：该漏洞由于SALT-NETAPI不正确地验证了EAUTH凭据和令牌导致，任何“ EAUTH”或“ TOKEN”的值都将允许用户绕过身份验证并调用SALT SSH。未经身份验证的用户可以访问针对Salt-SSH名册中设置的目标运行命令。

影响范围

SaltStack 2015/2016/2017/2018/2019/3000/3001/3002

修复方案

注意：安装升级前，请做好数据备份、快照和测试工作，防止发生意外

1. 升级至官方最新的软件版本：https://repo.saltstack.com

2. 设置SaltStack为自动更新，及时获取相应补丁

[参考链接](https://www.saltstack.com/blog/on-november-3-2020-saltstack-publicly-disclosed-three-new-cves/)

