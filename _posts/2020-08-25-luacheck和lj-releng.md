---
layout:     post   				    # 使用的布局（不需要改）
title:      luacheck and lj-releng                  # 标题
subtitle:   基本命令                        #副标题
date:       2020-08-25 				# 时间
author:     DYD 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - OpenResty
---

> 摘抄自OpenResty最佳实践

Lua 上下文中应当严格避免使用自己定义的全局变量。可以使用一个 lj-releng 工具来扫描 Lua 代码，定位使用 Lua 全局变量的地方。lj-releng 的相关链接：
https://github.com/openresty/openresty-devel-utils/blob/master/lj-releng

如果使用 macOS 或者 Linux，可以使用下面命令安装 lj-releng:

```bash
curl -L https://raw.githubusercontent.com/openresty/openresty-devel-utils/master/lj-releng > /usr/local/bin/lj-releng

chmod +x /usr/local/bin/lj-releng
```

然后进入你自己的 Lua 文件所在的工作目录，得到如下结果：
```bash

#  lj-releng
foo.lua: 0.01 (0.01)
Checking use of Lua global variables in file foo.lua...
op no.  line  instruction args  ; code
2  [8] SETGLOBAL 0 -1  ; A
Checking line length exceeding 80...
WARNING: No "_VERSION" or "version" field found in `use_foo.lua`.
Checking use of Lua global variables in file use_foo.lua...
op no.  line  instruction args  ; code
2  [1] SETGLOBAL 0 -1  ; A
7  [4] GETGLOBAL 2 -1  ; A
8  [4] GETGLOBAL 3 -1  ; A
18 [8] GETGLOBAL 4 -1  ; A
Checking line length exceeding 80...
```
结果显示： 在 foo.lua 文件中，第 8 行设置了一个全局变量 A ； 在 use_foo.lua 文件中，没有版本信息，并且第 1 行设置了一个全局变量 A ，第 4、8 行使用了全局变量 A 。当然，更推荐采用 luacheck 来检查项目中全局变量，之后的“代码静态分析”一节，我们还会讲到如何使用 luacheck。

```bash
sudo apt install lua-check

#ngx变量在开启了配置--std ngx_lua后可被luacheck识别
luacheck filename or directory即可
```

lj-releng文件
```bash
https://github.com/openresty/openresty-devel-utils/edit/master/lj-releng
```

[openresty OAuth 2  上](
https://www.jianshu.com/p/45093253b4f0)

[openresty OAuth 2 中](
https://www.jianshu.com/p/355807f5821d)

[openresty OAuth 2 下](
https://www.jianshu.com/p/ce6d59f823fc
)
[OAuth 2补充](
https://www.jianshu.com/p/aae7300568ca)

[OAuth介绍](
http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html)

[openresty最佳实践](
https://legacy.gitbook.com/book/moonbingbing/openresty-best-practices/details)

[api网关的选型和持续集成](
http://www.upyun.com/tech/article/485/API%20%E7%BD%91%E5%85%B3%E7%9A%84%E9%80%89%E5%9E%8B%E5%92%8C%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90.html)

[open talk 很多可以借鉴](
http://www.upyun.com/tech?topic=Opentalk&page=1)

[Travis CI教程](
http://www.ruanyifeng.com/blog/2017/12/travis_ci_tutorial.html)
