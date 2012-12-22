---
layout: post
title: ubuntu启动画面分辨率修改
---

自从装上了12.04后，启动画面和关机画面的像素一直停留在640x480，google了一下大概的修改方法。

第一步：修改/etc/default/grub文件

    $ sudo vi /etc/default/grub
    // 修改#GRUB_GFXMODE=640x480
    GRUB_GFXMODE=1024*768

第二步：修改/etc/grub.d/00_header文件

    $ sudo vi /etc/grub.d/00_header
    // 在set gfxmode = ${GRUB_GFXMODE}下添加
    set gfxpayload=keep

第三步：更新grub，重启

    $ sudo update-grub
    $ sudo restart


