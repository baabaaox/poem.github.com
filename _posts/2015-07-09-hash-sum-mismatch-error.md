---
layout: post
title: Hash Sum mismatch 错误
---

如果你在运行 sudo apt-get update 的时候出现 Hash Sum mismatch 错误提示，这个问题可能是你当前网络ISP数据缓存机制造成你系统需要更新的数据和实际得到的数据不一致造成无法通过数据校验检查,肯能你得到的数据只是ISP缓存的数据。<!-- more -->

### 解决方法

主要思路就是跳过当前网络，不通过当前网络之间获取数据，这里我们可以用VPN,代理软件来解决。

1.如果是全局代理，那么直接启用就可以正常更新了

2.如果是Goagent这样的软件,我们可以通过下面的命令来解决
    
    # 0.0.0.0:8080 是你代理软件监听的地址端口
    hulk@tahr:~$ sudo apt-get -o Acquire::http::proxy="http://0.0.0.0:8080/" update
