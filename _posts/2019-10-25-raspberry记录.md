---
layout:     post   				    # 使用的布局（不需要改）
title:      raspberry记录          # 标题
subtitle:                           #副标题
date:       2019-10-25 				# 时间
author:     DYD 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - raspberry
---
### 介绍
RPi硬件是SoC系统单芯片 CPU、GPU、DSP、SDRAM集成到一个芯片中。
RPi没有BIOS，配置信息保存在/boot/config.txt里。
官方系统raspbian系统，基于debian wheezy arm内核版本，桌面环境LXDE。
RPi很多应用是python开发的，外围硬件如GPIO、串口、I2C都可以通过python库函数编程。预装了python3和IDLE。
RPi启动慢主是要因为系统装在SD卡上，IO是主要瓶颈。
内置 scratch图形化编程开发环境，类似labview。是计算机教学工具。
调用RPi.GPIO库，可以编程控制GPIO等硬件接口。避免驱动开发的问题。

Raspberry Pi上预装有GCC编译器，可以进行C/C++编程开发。对于有经验的Linux开发者，如果把开发环境配置好，甚至可以直接用Raspberry Pi编译Linux
kernel，只不过速度很慢，据尝试过的人称，需要大约5小时以上。

官方提供的RPi.GPIO库主要针对的是Python编程，除此之外还有一些第三方库也非常好用，比如WiringPi，这是一款模仿Arduino Wiring风格的函数库，而
且支持C/C++、 Ruby、 Python、 Perl、Java、 TCL等多种语言编程，不局限于Python，使用起来非常简单，习惯C/C++编程的人可以通过这个库控制
Raspberry Pi的硬件接口。WiringPi还提供了附加的功能函数，如用于串口处理的shiftIn/shiftOut库（同时支持板载串口和USB转接的串口），用于控制LCD的库，简单的线程编程和进程优先级控制库，还完全支持PiFace扩展板。

### raspberry pi与arduino
Arduino是一个受欢迎的开放源硬体平台，使用的是微控制器， Raspberry Pi使用的是应用处理器，两者之间的配合还可以极大扩展应用和创意丰富性， RaspberryPi甚至能够成为Arduino的开发平台。
* Simon Monk的博客中提到了如何使用Python实现两者之间的通讯， Arduino会传送'Hello Pi'的讯号，而Raspberry Pi便会传送数字讯号给Arduino， Arduino便会根据该讯号闪耀LED特定的次数。
* Raspberry Pi方面，作者使用Python进行开发，使用特定的Python库——pySerial，这个库包含了Arduino的指令，可以存取串行口

### 状态灯
红灯应常亮，闪烁是电路出了问题。

绿灯闪烁，开机状态。

系统没后续动作，绿灯状态：微弱、熄灭不闪烁。再操作，绿灯会闪烁。

### 常用系统
* raspbian

* ubuntu mate

* kali linux

* ubuntu core 这个系统安全性高

### 源码下载

raspberry pi 官方文档，有可以参考的资料

[文档](https://github.com/raspberrypi/documentation)

[源码下载](https://github.com/raspberrypi)

### mac下烧系统的方法
插内存卡到电脑上
查看是否能被读取
```shell
df -lh
```
卸载sd卡
```shell
diskutil umount /dev/disk2s1
```
确认设备号
```shell
diskutil list
```
烧写系统
```shell
sudo dd bs=4m if=rpi_35_v6_1_2_3_jessie_kernel_4_4_50.img of=/dev/disk2
```
卸载
```shell
diskutil unmountDisk /dev/disk2
```

### 远程桌面
安装VNC
```shell
sudo apt-get install tightvncserver
```
启动
```shell
tightvncserver
```
设置密码，view-only设为no
再次启动
```shell
tightvncserver
```
Mac使用vnc viewer连接
[教程](https://www.realvnc.com/download/viewer/)

### 中文
去掉en_GB.UTF-8 UTF-8
选en_US.UTF-8 UTF-8
zh_CN.UTF-8 UTF-8
zh_CN.GBK GBK
重启，新版已经可以显示中文了。
老版还需要安装字库
```shell
sudo apt-get install ttf-wqy-zenhei ttf-wqy-microhei xfonts-wqy
sudo apt-get install scim-pinyin
sudo apt-get install scim-tables-zh
sudo apt-get install chromium-browser  chromium-l10n
```
查看主板温度
```shell
sudo /opt/vc/bin/vcgencmd measure_temp
```

### RPi截屏
```shell
sudo apt-get install scrot
scrot
```

### 时间校准

```shell
sudo ntpd -s -d
```

### 连接wifi
热点扫描
```shell
sudo iwlist wlan0 scan
```

编辑配置文件
```shell
sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

network={
    ssid="testing"
    psk="testingPassword"
}

```shell
wpa_cli -i wlan0 reconfigure
ifconfig wlan0
```

### 搭web服务

* LAMP(apache+mysql+php)
```shell
sudo apt-get install apache2
sudo apt-get install mysql-server
sudo apt-get install php5
sudo apt-get install php5-mysql
```
* LNMP(nginx+sqlite+php)
```shell
sudo apt-get install nginx
sudo apt-get install php5-fpm php5-sqlite
```

### 使用静态IP
```shell
cd /etc/network
sudo vi interfaces
iface eth0 inet static
address 192.168.1.10
netmask 255.255.255.0
gateway 192.168.1.1
```
或者直接在路由器里将mac与ip进行绑定

### SD卡备份
linux系统下,Mac系统只需把M改为小写m

备份
```shell
sudo dd bs=4M if=/dev/sdb of=raspbian.img
```

恢复
```shell
sudo dd bs=4M if=raspbian.img of=/dev/sdb
```

压缩备份
```shell
sudo dd bs=4M if=/dev/sdb | gzip > raspbian.img.gz
```

压缩恢复
```shell
gunzip --stdout raspbian.img.gz | sudo dd bs=4M of=/dev/sdb
```

### 其他
[python相关](https://github.com/raspberrypi/documentation/blob/master/linux/software/python.md)

[U盘做系统](https://github.com/raspberrypi/documentation/blob/master/hardware/raspberrypi/bootmodes/msd.md)

[远程访问的](https://github.com/raspberrypi/documentation/blob/master/remote-access/README.md)

### 查看版本

```shell
lsb_release -a
```

### 不用显示器连接raspberry
1. 格式化TF卡。
2. 刷入系统。
3. 在boot目录下创建SSH文件。
4. 网线直连电脑，将连接共享至直连网卡。
5. arp -a显示bridge即为直连网络。
6. ssh pi@192.168.2.2直连。
7. ssh登录后可做如下操作
    使用自带无线网卡连接wifi上网，连接后，可不需要直连。修改apt源，改成国内源。

    ```shell
    sudo apt-get install xrdp
    ```
    macos安装 Micro Remote Desktop

    安装远程桌面，使当前主机可以远程桌面连接树莓派。
    raspberry修改默认密码、扩展卡空间、修改location等配置。
    安装nginx、vim等。
    安装sslocal、privoxy等。
8. 配置妥当后，镜像备份，以备系统崩溃后使用。
9. 可以当成渗透测试平台用，也可当成ddos攻击目标使用。
10. 连接视频头，做人脸检测使用。

### raspberry 3B硬件配置
cpu:broadcom BCM2837

4 cores

1200 MHz

ram:1024M

ethernet 100M: 1个

wlan: broadcom BCM43438

wlan2.4GHz:b/g/n

wlan 5.0GHz:不支持

bluetooth:4.1

serial connection parameters: 115200/8N1

JTAG:Yes

Power:5VDC, 2.4A

[详细配置信息](https://openwrt.org/toh/hwdata/raspberry_pi_foundation/raspberry_pi_3_b)








