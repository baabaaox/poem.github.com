---
layout: post
title: 加固你的Ubuntu服务器
---

![Portgas D. Ace](http://ww4.sinaimg.cn/mw1024/6dc1b103gw1etho8cb49pj20i20b40vs.jpg)

现在CPU越来越快,内存越来越大,扫描工具的工作效率也越来越高,如何让我们的服务器变得安全一下,是一个值得持续讨论的话题.<!-- more -->

使用SSH公钥来对远程服务器进行身份验证相对于传统的密码登陆来说更加安全,因为很多扫描软件都是通过弱口令或者穷举碰撞这类方式来破解用户密码,另一方面由于登陆的不用输入密码,也可以防止中间人攻击

### 新建用户

1.在命令行里面通过SSH登陆到服务

    ssh root@server-address

2.新建一个用户账号
	
	adduser hulk

3.将该账号加入到系统管理员分组

    usermod -a -G sudo hulk

4.然后以root退出

    sudo logout

5.用新建的账号登陆

    ssh hulk@server-address

### 使用SSH Keys登陆

1.首先你得在你本地电脑上面生成SSH Keys

    ssh-keygen

2.上传你的公钥到服务器

     ssh-copy-id hulk@server-address

3.使用SSH Key 登陆

    ssh hulk@server-address

### 修改SSH端口,禁用SSH密码和root账号

1.打开SSH配置文件

    sudo vi /etc/ssh/sshd_config

2.修改默认端口为其他端口

    Port 2222

3.禁用SSH密码验证

    PasswordAuthentication no

4.禁用root用户

    PermitRootLogin no

5.只允许指定用户登录
 
    AllowUsers hulk

6.保存上面的修改退出编辑状态

    :wq

7.重启SSH服务

    sudo service ssh restart


8.在进行上面一切后，不要忙着退出，最好在另一个新窗口先试一试，如果无法登录的话在一步步检查自己哪里出了问题

    ssh hulk@server-address -p 2222

### 参考

* [https://linode.com/docs/security/securing-your-server/](https://linode.com/docs/security/securing-your-server/)