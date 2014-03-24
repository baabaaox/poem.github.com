---
layout: post
title: Ubuntu 处理文本文件奇技淫巧
---

7z

    sudo apt-get install p7zip-full
    文件打包
    7za a -t7z test.txt.7z test.txt
    目录打包
    7za a -t7z -r dir.7z /dir
    解压
    7z x test.txt.7z

磁盘信息

    df -hl

文件断点下载

    wget -i http://test.txt -c


文件内容察看，上百万行内容能没有他们？

    cat more less head tail sed

文件行数

     wc -l all20121224.txt

文本文件排序去重

    sort test.txt > sort.txt
    uniq sort.txt > uniq.txt


文本合并

    cat 2013* > 2013.txt
    cat 201301.txt 201302.txt > 2013.txt

文件分割

     split -l 1000000 hash.txt hash_
     wc -l *
