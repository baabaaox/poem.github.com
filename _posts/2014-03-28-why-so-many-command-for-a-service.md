---
layout: post
title: 为什么让一个服务器跑起来会用这么多命令？
---


!!!<!-- more -->

然后安装add-apt-repository命令，server版一般好像都自带了？

    sudo apt-get install python-software-properties

添加用到的源

    sudo add-apt-repository ppa:nginx/stable
    sudo add-apt-repository ppa:ondrej/php5

添加源后要记得更新，更新系统

    sudo apt-get update
    suod apt-get upgrade

安装nginx

    sudo apt-get install nginx

安装mysql，安装python-mysqlbd

    sudo apt-get install mysql-server-5.5
    sudo apt-get install python-mysqlbd

安装php

    sudo apt-get install php5 php5-cgi php5-cli php5-common php5-curl php5-fpm php5-gd php5-json php5-mcrypt php5-mysql

安装7z

    sudo apt-get install p7zip-full

安装git

    sudo apt-get install git

安装pip，必须的啊，顺道把源也改成豆瓣的

    sudo apt-get install python-pip

安装supervisor

    sudo pip install supervisor

安装tornado+torndb

    sudo pip install tornado
    sudo pip install torndb

安装mongodb

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
    echo 'deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen' | sudo tee /etc/apt/sources.list.d/mongodb.list
    sudo apt-get update
    sudo apt-get install mongodb-10gen

安装mongodb连接器

    sudo pip install mongo-connector
    如果上面没效果也许要用下面
    git clone https://github.com/10gen-labs/mongo-connector.git
    python setup.py install

安装solr

    sudo apt-get install openjdk-7-jdk
    sudo apt-get install tomcat7
    sudo mv solr.xml /etc/tomcat7/Catalina/localhost/solr.xml
    sudo chown tomcat7 /home/mongodb/solr/data


最后这几个是支援mongo-connector的

    sudo apt-get install libxml2-dev libxslt-dev
    sudo pip install lxml

大体上配置一次服务器我需要安装这些家伙，不知道哪天能用shell搞定？
