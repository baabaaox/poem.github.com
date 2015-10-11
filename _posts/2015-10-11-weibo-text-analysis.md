---
layout: post
title: 新浪微博文本分析
---

结合昨天写的把以前写过的一个微博文本分析脚本整理一下。<!-- more -->

![中国国家地理微博分析](http://ww3.sinaimg.cn/mw1024/6dc1b103jw1eztp6699i5j20rs0rswjy.jpg "中国国家地理微博分析")

只是抓取单用户的微博文本简单的进行了分词排序，然后提取热词绘制饼图，如果想更深入一步的可以用 Scrapy + Mongodb 来抓取更多的用户微博信息，在提取热词的时候可以根据词性来进一步优化热词的提取，再深入牵扯到语言处理方面就挺复杂的。

主要依赖的库

- [Requests](http://python-requests.org/){:target="_blank"}: 网络请求
- [BeautifulSoup](http://www.crummy.com/software/BeautifulSoup/){:target="_blank"}: HTML 解析
- [Jieba](https://github.com/fxsjy/jieba/){:target="_blank"}: 中文分词
- [Matplotlib](http://matplotlib.org/){:target="_blank"}: 绘制图表

### 代码

weibo.py 代码

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

        def get_info(self, target):
            '''
            获取微博信息
            '''
            req = self.session.get(target)
            soup = BeautifulSoup(req.text, 'lxml')
            data = {}
            data['title'] = soup.title.string
            data['page'] = int(soup.find('input', {'name': 'mp'}).get('value'))
            return data

        def fetch_sentence(self, target, count):
            '''
            获取微博
            '''
            sentences = []
            if count > 30:
                count = 30
            for i in xrange(1, count + 1):
                url = '%s?page=%s' % (target, i)
                req = self.session.get(url)
                soup = BeautifulSoup(req.text, 'lxml')
                items = soup.find_all('span', {'class': 'ctt'})
                for item in items:
                    sentences.append(item.get_text())
            return list(set(sentences))

        def analysis(self, sentences):
            '''
            分析微博
            '''
            import re
            import jieba
            import operator

            words = {}
            regx = ur'[^\u4e00-\u9fa5]+'
            for sentence in sentences:
                for word in jieba.cut(sentence):
                    if re.findall(regx, word) or len(word) < 2:
                        continue
                    if word in words:
                        words[word] += 1
                    else:
                        words[word] = 1
            words = sorted(
                words.items(),
                key=operator.itemgetter(1),
                reverse=True)[:20]
            return dict(words)

        def draw(self, title, url, words):
            '''
            绘制饼图
            '''
            import matplotlib
            matplotlib.use('Agg')
            import matplotlib.pyplot as plt

            matplotlib.rcParams['font.family'] = ['WenQuanYi Zen Hei']
            x = []
            labels = []
            explode = []
            for key in words.keys():
                x.append(words[key])
                labels.append(key)
                explode.append(0.1)
            explode = tuple(explode)
            plt.figure(1, figsize=(10, 10))
            plt.pie(
                x,
                explode=explode,
                labels=labels,
                colors=(
                    '#1ABC9C',
                    '#2ECC71',
                    '#3498DB',
                    '#9B59B6',
                    '#34495E',
                    '#F1C40F',
                    '#E67E22',
                    '#E74C3C',
                    '#ECF0F1',
                    '#95A5A6',
                ),
                autopct='%1.1f%%',
                shadow=True
            )
            plt.title(
                'Sina Weibo Analysis: %s \n %s' % (title, url),
                bbox={'facecolor': '0.8', 'pad': 16}
            )
            # plt.show()
            plt.savefig('analysis.png')


test.py 代码

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-

    import weibo

    WEIBO_ACCOUNT = 'Your weibo account'
    WEIBO_PASSWORD = 'Your weibo password'


    def main():
        url = 'http://weibo.cn/cng'
        w = weibo.Weibo(WEIBO_ACCOUNT, WEIBO_PASSWORD)
        data = w.get_info(url)
        sentences = w.fetch_sentence(url, data['page'])
        words = w.analysis(sentences)
        w.draw(data['title'], url, words)

    if __name__ == '__main__':
        main()
