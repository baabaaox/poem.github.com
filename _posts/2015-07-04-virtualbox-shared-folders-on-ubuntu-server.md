---
layout: post
title: Virtualbox 配置 Ubuntu Server 共享文件夹
---

测试环境为：Win8 Virtualbox-4.3.28 Ubuntu-14.04.2-server-amd64.<!-- more -->

### 安装dkms

    sudo apt-get install dkms

### 安装扩展

1.在虚拟机里面点击->设备->安装增强功能

2.挂载扩展镜像

    hulk@tahr:~$ sudo mount /dev/sr0 /media/cdrom

3.安装扩展

    hulk@tahr:~$ cd /media/cdrom
    hulk@tahr:~$ sudo ./VBoxLinuxAdditions.run

### 挂载共享文件到指定目录并开机自启动

1.挂载共享文件到指定目录

    hulk@tahr:~$ cd
    hulk@tahr:~$ mkdir workspace
    hulk@tahr:~$ sudo mount -t vboxsf workspace ./workspace/

2.开机自动挂载

    hulk@tahr:~$ sudo vi /etc/rc.local
    # 在exit 0 上一行加入
    mount -t vboxsf workspace /home/hulk/workspace/
