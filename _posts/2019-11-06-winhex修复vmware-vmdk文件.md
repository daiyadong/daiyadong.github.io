---
layout:     post   				    # 使用的布局（不需要改）
title:      winhex修复vmware-vmdk文件        # 标题
subtitle:                           #副标题
date:       2019-11-06 				# 时间
author:     DYD 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - winhex
    - vmware
---

虚拟机断电，vmx文件找不到，只有vmdk硬盘文件。
顺便吐槽下百毒，搜出来的方法99%扯淡。
害得我先要弄下科学冲浪。

winhex需要破解版的不能使用评估版

使用winhex修改vmdk文件，将CID与parentCID进行修改。winhex不能使用评估版的，评估版不能修改超过200K的文件。

![](https://wx2.sinaimg.cn/mw1024/00804KuLgy1g8o47fzrrmj30m00a9775.jpg)

注意，有过镜像备份的虚拟机，需要parent ID与最原始的版本ID要一致。比如我这里有三个文件，Ubuntu 16.vmdk是早的。
Ubuntu 16-0.vmdk是添加的第二块硬盘文件。
Ubuntu 16-000001.vmdk是一直在用的，这里新建虚拟机挂载此硬盘会提示父子ID不一致。所以才要上步修改ID的操作。

![](https://wx1.sinaimg.cn/mw1024/00804KuLgy1g8o47ft7qtj30go02xjrh.jpg)

修改完后，新建同类型虚拟机，添加硬盘，只挂载修改过的硬盘，可启动。

