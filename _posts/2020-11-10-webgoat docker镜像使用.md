---
layout:     post   				    # 使用的布局（不需要改）
title:      webgoat 与 dvwa docker镜像使用    # 标题
subtitle:                           #副标题
date:       2020-11-10 				# 时间
author:     DYD 				    # 作者
header-img: img/post-bg-debug.png 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 渗透
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

[dvwa低级教程](https://blog.csdn.net/weixin_42317232/article/details/103081044)

[dvwa中级教程](https://blog.csdn.net/weixin_42317232/article/details/103081043)

[dvwa高级教程](https://blog.csdn.net/weixin_42317232/article/details/103081042)
```bash
#拉取dvwa镜像
docker pull citizenstig/dvwa

#运行
docker run -p 80:80 -t citizenstig/dvwa

#登录用户名密码
admin
password
```

```bash
#WSL中tail -f没效果的解决办法
tail -f ---disable-inotify info.log
```