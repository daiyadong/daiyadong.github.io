---
layout:     post   				    # 使用的布局（不需要改）
title:     android adb调试与apk反编译 # 标题
subtitle:    #副标题
date:       2019-10-24 				# 时间
author:     DYD 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - android
    - apk
    - adb
---

1. 显示设备
```shell
adb devices
```

2. 使用root用户连接，需要root过的设备
```shell
adb root
```

3. 使用shell用户连接
```shell
adb connect 127.0.0.1:5554
```
```shell
adb shell
```
---
4. 使用dex2jar将dex文件反编译成jar包
```shell
d2j-dex2jar.bar classes.dex
```

5. 使用jd-gui.exe打开反汇编后的jar包
可查看类似Java 代码。

6. adb shell后过滤查找想找的包
```shell
pm list packages | grep daiyad
```
显示包的路径
```shell
pm path com.example.daiyd
```
提取apk包到本地
```shell
adb pull /data/app/xxxxxx/base.apk  ~/apks
```
7. 安装apk包到模拟器
```shell
adb install ./hhr.apk
```
8. 反编译apk安装包
解压缩
```shell
unzip test.apk
```
反编译
```shell
java -jar ../tools/apktool_2.3.3.jar d -f test.apk -o decompile
```



