---
layout: post
title: Ubuntu 时区设置
---

因为Ubuntu Server默认时区是使用UTC格式作为标准时间格式

    $ date -R

所以在使用计划任务时必须把时区切换过来

    $ sudo tzselect

按照提示进行选择时区，查看然后：

    # 添加 TZ='Asia/Shanghai'; export TZ 到 .profile
    $ vi .profile
