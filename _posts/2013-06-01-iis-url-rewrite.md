---
layout: post
title: IIS6下配置URL重写
---

2003 IIS6下配置URL重写，只能说都是坑。<!-- more -->

下载程序包和key

- 下载地址：https://www.dropbox.com/sh/hi9ah72bk0bdoqs/Yc_WYLK6qY
- 安装并且用key注册
- 此序列号适用于ISAPI Rewrite 2.9 Full

添加重写规制

修改ISAPI_Rerite目录下的 httpd.ini

    [ISAPI_Rewrite]
    # 3600 = 1 hour
    CacheClockRate 3600
    RepeatLimit 32

    RewriteRule .*\.(?:gif|jpg|png|css|js|txt|jpeg|swf|flv) $0 [I,L]
    RewriteRule /httpd(?:\.ini|\.parse\.errors) / [F,I,O]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^(?!/index.php)(?!/admin.php)(.*)$ /index.php/$1 [L]

这里只是重写了index.php/admin.php，静态资源必须加入第一个规制里不然无法显示。

配置

- 右键你的站点属性–ISAPI筛选器–添加–筛选器名称是ISAPI_Rewrite–可执行文件就是ISAPI_Rewrite.dll
- 重启IIS，ok
