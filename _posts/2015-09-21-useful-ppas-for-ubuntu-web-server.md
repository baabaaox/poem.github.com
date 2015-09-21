---
layout: post
title: 一些 Ubuntu Web 服务器常用的 PPA
---

![干物妹小埋](http://ww3.sinaimg.cn/mw1024/6dc1b103gw1ewa7duqnfqj20i20b4wgk.jpg)

PPA,表示 Personal Package Archives,也就是个人软件包集.<!-- more -->下面是一些我收集的PPA.

### Nginx

    ppa:nginx/stable

### MySQL

    # For MySQL 5.7
    ppa:ondrej/mysql-5.7
    # For MySQL 5.6
    ppa:ondrej/mysql-5.6
    # For MySQL 5.5
    ppa:ondrej/mysql-5.5

### PHP

    # For PHP 7.0
    ppa:ondrej/php7.0
    # For PHP 5.6
    ppa:ondrej/php5-5.6
    # For PHP 5.5
    ppa:ondrej/php5
    # For PHP 5.4
    ppa:ondrej/php5-oldstable

### MongoDB

1.导入 MongoDB 的 GPG 签名秘钥到 APT 密钥圈

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10

2.添加 MongoDB 到你的程序源列表

    # Ubuntu 12.04
    echo "deb http://repo.mongodb.org/apt/ubuntu precise/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list
    # Ubuntu 14.04
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list

3.更新软件列表并安装 MongoDB

    sudo apt-get update && sudo apt-get install -y mongodb-org

### Scrapy

1.导入 Scrapy 的 GPG 签名秘钥到 APT 密钥圈

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 627220E7

2.添加 Scrapy 到你的程序源列表

    echo 'deb http://archive.scrapy.org/ubuntu scrapy main' | sudo tee /etc/apt/sources.list.d/scrapy.list

3.更新软件列表并安装 Scrapy

    sudo apt-get update && sudo apt-get install scrapy
    # Ubuntu 14.04 可能还要执行下面操作
    sudo pip install service-identity
    sudo pip install pyasn1 --upgrade


### 参考

* [http://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/](http://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/){:target="_blank"}
* [http://doc.scrapy.org/en/latest/topics/ubuntu.html#topics-ubuntu](http://doc.scrapy.org/en/latest/topics/ubuntu.html#topics-ubuntu){:target="_blank"}
