---
layout: post
title: 经典算法之快速排序
---

快速排序主要要掌握的思想是分治和迭代。<!-- more -->

* 取一个数出来作为基准，这个数可以是数列里面任意位置的数。
* 新建两个容器，把数列里面剩余的数与基准进行比较，小于的放第一个容器，大于的放第二个容器。
* 递归合并基准和两个容器，直到分割的数列只包含一个数。

下面是该算法python的实现：

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-

    import random

    def qsort(L):
         if len(L) <= 1: return L
         return qsort([lt for lt in L[1:] if lt < L[0]]) + L[0:1] + qsort([gt for gt in L[1:] if gt >= L[0]])

    L =  range(2, 100, 2)
    random.shuffle(L)
    print qsort(L)

下面是该算法PHP的实现:

    <?php
    function quick_sort($array) {
        $size = count($array);
        if (1 < $size) {
            $first = $array[0];
            $left = $right = array();
            for ($i = 1; $i < $size; $i++) {
                if ($first > $array[$i]) {
                    $left[] = $array[$i];
                } else {
                    $right[] = $array[$i];
                }
            }
            return array_merge(quick_sort($left), array($first), quick_sort($right));
        } else {
            return $array;
        }
    }

    $array = range(0, 100, 2);
    shuffle($array);
    $result = quick_sort($array);
    print_r($result);
    ?>

