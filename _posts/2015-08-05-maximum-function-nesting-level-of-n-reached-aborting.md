---
layout: post
title: Xdebug限定程序递归深度
---

"PHP message: PHP Fatal error:  Maximum function nesting level of '256' reached, aborting!".<!-- more -->

今天在写一个排序,调试的时候出现上面错误,排序方法如下:

    public static function quick_sort_by_created_at($array)
    {
        $size = count($array);
        if (1 < $size) {
            $first = $array[0];
            $left = $right = array();
            for ($i = 1; $i < $size; $i++) {
                if ($first->created_at < $array[$i]->created_at) {
                    $left[] = $array[$i];
                } else {
                    $right[] = $array[$i];
                }
            }
            return array_merge(self::quick_sort_by_created_at($left), array($first), self::quick_sort_by_created_at($right));
        } else {
            return $array;
        }
    }

查了下是由于Xdebug默认允许的嵌套程序的最大访问深度为100,而我上面方法里面使用了递归,并且在程序里面调用运行时访问深度超过了这个值.但是由于这只是Xdebug的限制,而不是PHP本身的限制,解决方法:修改一下配置参数重启php服务即可.

    $ sudo vi /etc/php5/fpm/conf.d/20-xdebug.ini
    // 加上下面这行,限定递归深度为500
    xdebug.max_nesting_level = 500
    $ sudo service php5-fpm restart

参考: [Solution for “Fatal error: Maximum function nesting level of '100' reached, aborting!” in PHP](http://stackoverflow.com/questions/8656089/solution-for-fatal-error-maximum-function-nesting-level-of-100-reached-abor)
