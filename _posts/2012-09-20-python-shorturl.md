---
layout: post
title: 短网址的python实现
---

与，右移，补码，反码，对我来说已经是很冷的知识了

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-

    import random
    import hashlib


    def shorturl(url):
        chars = 'abcdefghijklmnopqrstuvwxyz0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'
        _hex = 0x7ffffff & int(str(hashlib.md5(url).hexdigest()), 16)
        code = ''
        for i in range(9):
            index = 0x0000003d & _hex
            code += chars[index]
            _hex = _hex >> 3
        return code


    def main():
        print shorturl(str(random.randint(1000, 9999)))

    if __name__ == '__main__':
        main()
