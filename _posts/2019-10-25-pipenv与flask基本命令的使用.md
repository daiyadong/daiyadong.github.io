---
layout:     post   				    # 使用的布局（不需要改）
title:     pipenv与flask基本命令的使用 # 标题
subtitle:   #副标题
date:       2019-10-25 				# 时间
author:     DYD 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - pipenv
    - flask
---

显示所有可选项
```shell
pipenv 
```



选择python版本

```shell
pipenv --three
```

```shell
pipenv --two
```

显示虚拟环境信息

```shell
pipenv --venv
```


安装开发环境需要的依赖

```shell
pipenv install
```

安装调试时用的包
```shell
pipenv install --dev
```

指定安装源
```shell
pipenv install flake8 --dev --pypi-mirror https://mirrors.aliyun.com/pypi/simple
```

图形化显示包依赖

```shell
pipenv graph
```


生成Pipfile Pipfile.lock文件

```shell
pipenv install
```


进入虚拟环境

```shell
pipenv shell
```


flask shell进入，类似python shell的交互环境

```shell
flask shell
```


运行flask，该运行模式不能被外界访问到

```shell
flask run
```


添加--host选项，可被外界主机访问，默认端口是5000

```shell
flask run --host 0.0.0.0
```


指定端口运行，默认端口是5000

```shell
flask run --host 0.0.0.0 --port 5000
```
