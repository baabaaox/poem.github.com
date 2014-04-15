---
layout: post
title: 经典算法之插入排序
---

插入排序（Insertion Sort）的算法描述是一种简单直观的排序算法。它的工作原理是通过构建有序序列，对于未排序数据，在已排序序列中从后向前扫描，找到相应位置并插入。<!-- more -->

- 从第一个元素开始，该元素可以认为已经被排序
- 取出下一个元素，在已经排序的元素序列中从后向前扫描
- 如果该元素（已排序）大于新元素，将该元素移到下一位置
- 重复步骤3，直到找到已排序的元素小于或者等于新元素的位置
- 将新元素插入到该位置后
- 重复步骤2~5

下面是该算法的php实现：

    <?php
    function insertion_sort($array) {
        foreach ($array as $key=>$value) {
            $i = $key - 1;
            while ($i >= 0 && $array[$i] > $value) {
                list($array[$i], $array[$i+1]) = array($array[$i+1], $array[$i]);
                $i--;
            }
        }
        return $array;
    }

    $array = range(2, 100, 2);
    shuffle($array);
    $result = insertion_sort($array);
    print_r($result);
