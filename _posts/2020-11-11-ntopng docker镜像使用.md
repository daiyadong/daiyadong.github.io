---
layout:     post   				    # 使用的布局（不需要改）
title:      ntopng docker镜像使用    # 标题
subtitle:                           #副标题
date:       2020-11-11 				# 时间
author:     DYD 				    # 作者
header-img: img/post-bg-debug.png	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - ntopng
---


ntopng docker镜像方式使用

```bash
#拉取ntopng镜像
docker pull ntop/ntopng:stable

#运行ntopng镜像
docker run --net=bridge -t -p 3000:3000 ntop/ntopng:stable
```

涉及到DPI相关技术，有时间可以进行深入研究