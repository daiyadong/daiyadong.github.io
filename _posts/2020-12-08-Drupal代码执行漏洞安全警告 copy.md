---
layout:     post   				    # 使用的布局（不需要改）
title:      Drupal 代码执行漏洞安全警告                # 标题
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
CVE编号 CVE-2020-13671

漏洞详情
Drupal官方通报了一个Drupal任意文件上传漏洞，该漏洞使远程攻击者可以破坏易受攻击的系统。由于Drupal core 没有正确地处理上传文件中的某些文件名，远程攻击者通过上传恶意文件，在某些特定的配置下可能会被当作 php 解析，并在服务器上执行该文件，从而导致远程代码执行。

影响范围
Drupal 7系列，版本号< 7.74

Drupal 8.8系列，版本号< 8.8.11

Drupal 8.9系列，版本号< 8.9.9

Drupal 9.0系列，版本号< 9.0.8

修复方案
注意：安装升级前，请做好数据备份、快照和测试工作，防止发生意外

1、Drupal  升级到最新版本；
Drupal 7.74
Drupal 8.8.11
Drupal 8.9.9
Drupal 9.0.8

2、通过安装hids 检测发现攻击者上传的恶意木马、PHP文件；

[参考链接](
https://www.drupal.org/sa-core-2020-012)
