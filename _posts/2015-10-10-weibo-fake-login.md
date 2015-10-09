---
layout: post
title: 新浪微博模拟登陆
---

关于新浪微博模拟登陆网络上面已经有很多文章了，这里我主要介绍一下实现的大概流程。<!-- more -->


### 思路

对于任何网站我们尝试方向都应该是：APP->Mobile->Desktop。一般来说很多网站的 APP API 接口都是没有进行
加密，使用 API 接口直接操作数据可谓事半功倍，但是BAT大都对数据进行了加密；其次是移动端网站；最后是桌面版网站。

### 抓包

- 如果要对手机上面的APP进行抓包可以用 [Fiddler](https://www.telerik.com/download/fiddler){:target="blank"}
- 如果要对电脑上面的APP进行抓包可以用 [Wireshark](https://www.wireshark.org/){:target="blank"}

上面两个都是非常棒的抓包工具

这次我们已移动端作为突破口，[weibo.cn](http://weibo.cn) 这个网址，所有采用 Wireshark 进行抓包，渣浪这个页面真的很朴素

![login page](http://ww4.sinaimg.cn/mw1024/6dc1b103jw1ezsixl3iblj20gd061dgw.jpg '登陆页面')

![source](http://ww3.sinaimg.cn/mw1024/6dc1b103jw1ezsjyoz02mj20vr0e643n.jpg '页面源码')

过滤出我们需要的东西

![wireshark](http://ww4.sinaimg.cn/mw1024/6dc1b103jw1ezsiywusakj20si0lsgv8.jpg "Wireshark 2.0")


### 实现

通过抓包我们得到了登陆点和表单内容后就可以写代码了

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-


    import os
    import requests
    from bs4 import BeautifulSoup
    from cookielib import LWPCookieJar

    COOKIE_FILE = 'cookiejar'
    CDN_URL = 'http://ww3.sinaimg.cn'
    LOGIN_URL = 'http://login.weibo.cn/login/'
    UPLOAD_URL = 'http://m.weibo.cn/mblogDeal/addPic'
    REFERER_URL = 'http://m.weibo.cn'


    class Weibo():
        def __init__(self, account, password):
            '''
            初始化
            '''
            session = requests.Session()
            session.cookies = LWPCookieJar(COOKIE_FILE)
            self.session = session
            self.account = account
            self.password = password
            if not os.path.exists(COOKIE_FILE):
                self.login()
            else:
                self.session.cookies.load()

        def login(self):
            '''
            登陆
            '''
            req = self.session.get(LOGIN_URL)
            soup = BeautifulSoup(req.text, 'lxml')
            action = '%s%s' % (LOGIN_URL, soup.find('form').get('action'))
            items = soup.find_all('input')
            data = {}
            for index, item in enumerate(items):
                name = item.get('name')
                value = item.get('value')
                if (0 == index):
                    data[name] = self.account
                elif (1 == index):
                    data[name] = self.password
                elif (2 == index):
                    data[name] = 'on'
                else:
                    data[name] = value
            print data
            self.session.post(action, data=data)
            self.session.cookies.save()
            print 'Login success'

        def fetch(self, url):
            '''
            抓取远程图片内容
            '''
            req = requests.get(url)
            return req.content

        def put(self, content):
            '''
            保存图片
            '''
            headers = {
                'Referer': REFERER_URL
            }
            data = {
                'type': 'json'
            }
            files = {
                'pic': (
                    'test',
                    content,
                    'image/jpeg'
                )
            }
            req = self.session.post(
                UPLOAD_URL,
                headers=headers,
                data=data,
                files=files
            )
            try:
                data = req.json()
                return '%s/mw1024/%s.jpg' % (CDN_URL, data['pic_id'])
            except Exception:
                print req.text
                return False

### 备注

- 如果登陆页面出现验证码你可能要自己搞定，经常使用的 ip 一般不会出现验证码
- 上面的图片上传接口比较容易使用但是每天图片上传数量有限制
