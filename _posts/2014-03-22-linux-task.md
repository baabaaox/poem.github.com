---
layout: post
title: Linux 计划任务
---

无论是windows还是linux，计划任务仍然是管理服务器很重要的一个工具。<!-- more -->

at：在未来的某一时间执行命令[链接](http://manpages.ubuntu.com/manpages/hardy/man1/at.1posix.html)

crontab：为个人用户维护定时时任务文件[链接](http://manpages.ubuntu.com/manpages/precise/en/man1/crontab.1.html)
/etc/crontab 文件指定 Cron 应该将哪些作业作为系统 Cron 作业运行。通常来讲，该文件告诉 Cron 分别按照每小时、每天、每周和每月的时间间隔运行位于 /etc/cron.hourly、/etc/cron.daily、/etc/cron.weekly 和 /etc/cron.monthly 中的脚本。

crontab的格式如下面：

    f1 f2 f3 f4 f5 program
    其中 f1 是表示分钟，f2 表示小时，f3 表示一个月份中的第几日，f4 表示月份，f5 表示一个星期中的第几天。program 表示要执行程式的路径。
    当 f1 为 * 时表示每分钟都要执行 program，f2 为 * 时表示每小时都要执行程式，其余类推
    当 f1 为 a-b 时表示从第 a 分钟到第 b 分钟这段时间内要执行，f2 为 a-b 时表示从第 a 到第 b 小时都要执行，其余类推
    当 f1 为 */n 时表示每 n 分钟个时间间隔执行一次，f2 为 */n 表示每 n 小时个时间间隔执行一次，其余类推
    当 f1 为 a, b, c,... 时表示第 a, b, c,... 分钟要执行，f2 为 a, b, c,... 时表示第 a, b, c...个小时要执行，其余类推

anacron：Cron的补充[链接](http://www.ibm.com/developerworks/cn/linux/l-anacron/)
