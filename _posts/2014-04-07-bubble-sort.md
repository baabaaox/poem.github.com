---
layout: post
title: 经典算法之冒泡排序
---

冒泡排序通过遍历数列，比较相邻两个数字间的大小，如果它们之间的位置错误就将其位置交换过来。最后小的元素会经过交换慢慢浮到数列顶端，所以称之为冒泡。<!-- more -->

下面是该算法的Python实现：

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-

    import random

    def bubble_sort(list_x):
        len_x = len(list_x) - 1
        for i in range(0, len_x):
            for j in range(0, len_x):
                if (list_x[j] > list_x[j+1]):
                    list_x[j], list_x[j+1] = list_x[j+1], list_x[j]
        return list_x

    list_a =  range(2, 100, 2)
    random.shuffle(list_a)
    print bubble_sort(list_a)


下面是该算法的PHP实现：

    <?php
    function bubble_sort($array) {
        $size = count($array);
        for ($i = 0; $i < $size; $i++) {
            for ($j = 1; $j < $size; $j++) {
                if($array[$j] < $array[$j-1]) {
                    list($array[$j-1], $array[$j]) = array($array[$j], $array[$j-1]);
                }
            }
        }
        return $array;
    }

    $array = range(2, 100, 2);
    shuffle($array);
    $result = bubble_sort($array);
    print_r($result);
    ?>
