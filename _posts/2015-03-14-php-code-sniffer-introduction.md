---
layout: post
title: PHP_CodeSniffer 介绍
---

PHP_CodeSniffer 主要用来检测 PHP 代码是否违反指定的编码标准，可以方便大家在同一项目中的编码风格保持一致<!-- more -->

### 安装

通过 PEAR 安装

    $ sudo pear install PHP_CodeSniffer

### 使用

查看内置有哪些编码标准

    $ phpcs -i
    The installed coding standards are PSR2, MySource, Zend, PSR1, PHPCS, Squiz and PEAR

新增 Symfony2 编码标准

    $ git clone git://github.com/escapestudios/Symfony2-coding-standard.git
    $ sudo mv ./Symfony2-coding-standards/Symfony2 /usr/share/php/PHP/CodeSniffer/Standards
    $ phpcs -i
    The installed coding standards are PSR2, MySource, Zend, PSR1, PHPCS, Squiz, PEAR and Symfony2


指定编码标准为 Symfony2 进行检测

    $ phpcs -n --standard=Symfony2 /workspace/YourPHPCode.php

指定检测报告输出类型: "full", "xml", "checkstyle", "csv", "json", "emacs", "source", "summary", "diff"

    $ phpcs -n --report=checkstyle --standard=Symfony2 /workspace/YourPHPCode.php

### PHP Coding Standards Fixer

PHP_CodeSniffer 虽然可以帮助我们找出不符合编码标准的代码, 但是如果我们一个原本没有遵守任何规范的项目突然要遵守某一规范的话，我们不可能一个文件一个文件的去修改，这时我们就需要用 [PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer){:target="_blank"} 这样的工具来自动的帮我们安装编码规范去修复代码

安装

    $ wget -c http://get.sensiolabs.org/php-cs-fixer.phar -O php-cs-fixer
    $ sudo chmod a+x php-cs-fixer
    $ sudo mv php-cs-fixer /usr/local/bin/php-cs-fixer
    $ whereis php-cs-fixer
    php-cs-fixer: /usr/local/bin/php-cs-fixer

更新

    $ sudo php-cs-fixer self-update

使用

    $ php-cs-fixer fix /workspace/project --level=symfony
