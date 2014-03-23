---
layout: post
title: Mysql定时备份
---

主要是利用crontab+shell。<!-- more -->

    #!/bin/bash

    dir='/home/backup/mysql/'
    name=`date +%F`'.sql'

    echo '开始备份数据...'
    mysqldump --add-drop-database --add-drop-table --all-databases | gzip > $dir$name'.gz'
    echo '删除10天前的备份...'
    old_file=$dir`date +%F --date='10 days ago'`'.*'
    rm -fr $old_file

然后就是配置corntab，每天四点过一分进行备份

    sudo crontab -e

    01 04 * * * /home/backup/msyqlbackup.sh

    sudo crontab start/restart

默认mysql用户名密码

    sudo vi /etc/mysql/my.cnf

    [client]
    port            = 3306
    socket          = /var/run/mysqld/mysqld.sock
    user            = root
    password        = HardM0de
