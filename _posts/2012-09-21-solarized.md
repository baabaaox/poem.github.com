---
layout: post
title: 设置Solarized配色方案
---

[Sublime](http://www.sublimetext.com/ "SublimeText")在**ubuntu**下面写东西很不爽，中文输入让人不爽到了极点！所以写点东西
感觉还是vim爽啊

在找主题的时候，在[官网](http://www.vim.org/ "Vim")挖坟的时候一下子就把
[Solarized](http://www.vim.org/scripts/script.php?script_id=3520 "Solarized")挖到起了，太火了！太具有艺术气息了

以下是今日收获

[vim-colors-solarized](https://github.com/altercation/vim-colors-solarized)
是Solarized的vim主题

下载

    $ git clone git://github.com/altercation/vim-colors-solarized.git
    $ mv vim-colors-solarized/colors/solarized.vim ~/.vim/colors/

设置

    set t_Co=16
    syntax on
    set background=dark
    colorscheme solarized

[gnome-terminal-colors-solarized](https://github.com/sigurdga/gnome-terminal-colors-solarized) gnome终端的Solarized配色方案。

步骤

    $ git clone git://github.com/sigurdga/gnome-terminal-colors-solarized.git
    $ cd gnome-terminal-colors-solarized
    $ ./install.sh

