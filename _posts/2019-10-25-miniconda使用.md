---
layout:     post   				    # 使用的布局（不需要改）
title:      miniconda使用 # 标题
subtitle:                           #副标题
date:       2019-10-25 				# 时间
author:     DYD 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - miniconda
    - docker
---

### docker镜像miniconda使用
[docker-miniconda介绍](https://hub.docker.com/r/continuumio/miniconda3)

从docker hub拉取miniconda
```shell
docker pull continuumio/miniconda3
```

进入交互模式
```shell
docker run -i -t continuumio/miniconda3 /bin/bash
```

使用jupyter notebook
```shell
docker run -i -t -p 8888:8888 continuumio/miniconda3 /bin/bash -c "/opt/conda/bin/conda install jupyter -y --quiet && mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser"
```
使用浏览器访问

http://localhost:8888 or http://<docker-machine-ip>:8888

### 手动安装方式
[miniconda手动安装](https://conda.io/en/master/miniconda.html)

升级环境
```shell
conda env update -f environment.yml
```

激活
```shell
conda activate gluon
```

反激活
```shell
conda deactivate
```

### jupyter notebook不能远程访问的问题

生成配置文件

```shell
jupyter notebook --generate-config
```
会写配置文件到: /home/dyd/.jupyter/jupyter_notebook_config.py
```shell
jupyter notebook password
```
会生成密码文件到 ~/.jupyter/jupyter_notebook_config.json
修改py文件，将remote_access访问打开即可。

> c.NotebookApp.ip='*'    #163行

> c.NotebookApp.password = u'sha:ce...刚才复制的那个密文' #217行

> c.NotebookApp.open_browser = False#208

> c.NotebookApp.port =8888 #可自行指定一个端口, 访问时使用该端口228行

这四条是不是必须的还不知道。现在已可用。

[可以参考的方法](https://www.cnblogs.com/wu-chao/p/8419889.html)





