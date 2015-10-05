---
layout: post
title: Sublime Text 3 常用包
---

本文主要介绍一些使用 Sublime Text 作为开发工具常使用的包 <!-- more -->

### Seti_UI

[Seti_UI](https://packagecontrol.io/packages/Seti_UI){:target="_blank"}是一款 Sublime Text 3 主题

#### 截图

Seti.sublime-theme
![Seti.sublime-theme](http://ww3.sinaimg.cn/mw1024/6dc1b103jw1ezqqt56qsqj21ao0r9jtv.jpg)

Seti_orig.sublime-theme
![Seti_orig.sublime-theme](http://ww3.sinaimg.cn/mw1024/6dc1b103jw1ezqqscbmmsj21ao0r976s.jpg)

#### 配置

    {
        "theme": "Seti.sublime-theme"
    }

### Side​Bar​Enhancements

[Side​Bar​Enhancements](https://packagecontrol.io/packages/SideBarEnhancements){:target="_blank"} 主要是对 Sublime Text 侧边栏进行功能增强

#### 截图

![Side​Bar​Enhancements](http://ww3.sinaimg.cn/mw1024/6dc1b103jw1ezqroz0p80j209u0l2mzg.jpg)

### InputHelper

[InputHelper](https://github.com/xgenvn/InputHelper){:target="_blank"} Ubuntu 下面中文输入解决方案

#### 截图

![InputHelper](http://ww1.sinaimg.cn/mw1024/6dc1b103jw1ezqs1kfuy6j20ev083dg3.jpg)

#### 手动安装

这里推荐手动安装，通过 Package Control 安装可能无法正常使用

    $ cd ~/.config/sublime-text-3/Packages
    $ git clone https://github.com/xgenvn/InputHelper.git

### Emmet

[Emmet for Sublime Text](https://github.com/sergeche/emmet-sublime){:target="_blank"} 是 [Emmet](http://emmet.io/){:target="_blank"} 官方对 Sublime 的支持插件，能大大的提高编写 HTML & CSS 工作效率

### Terminal

[Terminal](https://packagecontrol.io/packages/Terminal){:target="_blank"} 让你轻松的从选中文件夹启动 Terminal

### DocBlockr

[DocBlockr](https://packagecontrol.io/packages/DocBlockr){:target="_blank"} 让你更方便的为你的 Javascript, PHP, CoffeeScript, Actionscript, C & C++ 代码编写文档

### Git Gutter

[Git Gutter](https://packagecontrol.io/packages/GitGutter){:target="_blank"} 会显示相应文件版本变动信息

#### 截图

![Git Gutter](http://ww1.sinaimg.cn/mw1024/6dc1b103jw1ezqstvm2xlj208304x74r.jpg)

### CTags

[CTags](https://packagecontrol.io/packages/CTags){:target="_blank"} 让 Sublime Text 支持 [Exuberant CTags](http://ctags.sourceforge.net/){:target="_blank"} 从而达到快速定位功能


#### Exuberant CTags 安装

    # Ubuntu
    $ sudo apt-get install exuberant-ctags

### Python Flake​8 Lint

[Python Flake8 Lint](https://packagecontrol.io/packages/Python%20Flake8%20Lint){:target="_blank"} 方便的对 Python 代码进行  PEP8, PEP257, PyFlakes, mccabe and pep8-naming 风格检查

### Phpcs

[Git Gutter](https://packagecontrol.io/packages/Phpcs){:target="_blank"} 让 Sublime Text 支持 PHP CodeSniffer, PHP Coding Standard Fixer, Linter and Mess Detector，这个插件对应编写 PHP 程序意义非凡
