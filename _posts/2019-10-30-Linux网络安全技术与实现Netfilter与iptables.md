---
layout:     post   				    # 使用的布局（不需要改）
title:      Linux网络安全技术与实现Netfilter与iptables          # 标题
subtitle:                           #副标题
date:       2019-10-30 				# 时间
author:     DYD 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Linux
    - iptables
    - netfilter
---

### 发展
kernel 2.0       ipfwadm
kernel 2.2       ipchains
kernel 2.4/2.6   Netfilter/iptables

[netfilter网址](https://www.netfilter.org)

### 内核模块存放目录

netfilter内核模块所在目录
/lib/modules/kerne_version/kernel/net/ipv4/netfilter
/lib/modules/kerne_version/kernel/net/ipv6/netfilter

现在不分ipv4与ipv6版本目录为
/lib/modules/kerne_version/kernel/net/netfilter

### 规则
![](https://i.postimg.cc/SRtVcJVZ/00804-Ku-Lgy1g8gbwygdw3j30bf0gbgn6.jpg)
有四个表
* filter
* nat
* mangle
* raw

filter：最重要的机制，执行数据包过滤，防火墙的作用。

nat: network address translation 网络地址转换功能，防火墙不可缺少。

mangle:修改数据包的内容

raw:加愉数据包穿过防火墙的速度，提高性能。

### 规则匹配方式
* first match
* 全部不匹配时，走默认的策略

### 应用层iptables相关
![](https://i.postimg.cc/1zxCWVS2/00804-Ku-Lgy1g8gbwyg9vpj30iw0gdmxm.jpg)

### iptables基本语法规则
iptables命令格式:
iptables -t TABLE -操作式 规则条件

iptables -A INPUT -p icmp -s 192.168.0.200 -j DROP

-p icmp、-p udp、-p tcp、-p all

-s 源地址

-d 目标地址

处理方式有 ACCEPT,DROP,REJECT

```
iptables -A INPUT -p udp -s 192.168.0.200 --dport 53 -j REJECT
--dport 目标端口
--sport 源端口
指明端口时一定要指明协议

iptables -A INPUT -p all -s 192.168.1.0/24 -d 192.168.0.1 -j ACCEPT
设置一个网段的规则

iptables -A INPUT -p tcp -i eth1 --dport 22 -j ACCEPT
指明网口 -i eth1、-o eth2

iptables -A OUTPUT -o eth0 -p tcp -d ! edu.uuu.com.cn --dport 80 -j REJECT
不允许本机从eth0口访问

iptables -A FORWARD -i eth1 -o eth0 -p tcp --dport 80 -j DROP
不允许访问外网
```

```
例
1、列出filter表内容
iptables -t filter -L
2、列出filter表中INPUT链内容
iptables -t filter -L INPUT
3、清除filter表中内容
iptables -t filter -F
4、添加规则到filter表INPUT链
iptables -t filter -A INPUT -p icmp -j ACCEPT
5、将FORWARD链默认策略设置为丢弃
iptables -t filter -P FORWARD DROP
6、在INPUT链中插入新规则
iptables -t filter -I INPUT 2 -p tcp -j ACCEPT
7、取代INPUT链中己经存在的规则
iptables -t filter -R INPUT 2 -p tcp -j ACCEPT
8、删除INPUt链中存在的规则
iptables -t filter -D INPUT 2
```

### 连接状态
四种
* ESTABLISHED
* NEW
* RELATED
* INVALID
这四种状态与TCP/IP的十二种状态无关系

#### 与ESTABLISHED的关系
与tcp包关系
防火墙上运行ssh client，如果request包能穿过墙，那来回方向数据包都是ESTABLISHED
与udp包关系
防火墙上解析DNS，如果request能穿过，来回方向都是ESTABLISHED
与icmp包关系
如果第一个icmp包能穿过，来回都是

对应设置iptables命令是:
```
iptables -A INPUT -p tcp -m state --state ESTABLISHED -j ACCEPT
```

#### 与NEW的关系
NEW与协议无关，其所指的是每一条连接中的第一个数据包。包括tcp,udp,icmp

#### 与RELATED的关系
related状态数据包其含义是指被动产生的应答数据包，而且这个数据包不属于现在的任何连接。
如trace 命令，主机发出的是tcp包，回来的是icmp包。
relate状态数据包与协议无关，只要应答的数据包是因为本机先送出一个数据包而导致另一条连接的产生
， 那么这个新连接的所有数据包都属于related状态

#### INVALID
状态不明的数据包。
iptables -A INPUT -p all -m state --state INVALID -j DROP

规则的位置很重要

### 管理规则
#### 系统自带方法
service iptables save 保存规则
chkconfig iptables on 重启后自动应用规则
缺点:不好修改
#### 使用shell脚本管理
写好后写入到/etc/rc.d/rc.local开机启动执行
