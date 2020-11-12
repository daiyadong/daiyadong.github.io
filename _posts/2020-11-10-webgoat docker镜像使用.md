---
layout:     post   				    # 使用的布局（不需要改）
title:      webgoat docker镜像使用    # 标题
subtitle:                           #副标题
date:       2020-11-10 				# 时间
author:     DYD 				    # 作者
header-img: img/post-bg-debug.png 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - OpenResty
---

[webgoat使用解析](https://www.bbsmax.com/A/B0zq1OPnzv/)


```bash
#拉取webgoat镜像
docker pull webgoat/webgoat-7.1 

#运行webgoat
docker run -p 8080:8080 -t webgoat/webgoat-7.1

#登录
localhost:8080/WebGoat
user: webgoat
password: webgoat

```

```bash
#WSL中tail -f没效果的解决办法
tail -f ---disable-inotify info.log
```