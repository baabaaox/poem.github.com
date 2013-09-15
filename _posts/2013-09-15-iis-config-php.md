---
layout: post
title: IIS7.5下配置php5.5
---

IIS7.5下php生成环境配置备忘。<!-- more -->

安装PHP

1. 注意事项
    * 如果是用于 IIS 则选择 PHP 5.3 VC9 Non Thread Safe 或者 VC6 Non Thread Safe
    * 如果是用 IIS7 或更高版本以及 PHP 5.3+，则应选择 VC9 的包
    * VC9 版本是用 Visual Studio 2008 编译的并且在性能和稳定性上都有所提高。VC9 版本需要用户系统中安装有 » Microsoft 2008 C++ Runtime (x86) 或者 » Microsoft 2008 C++ Runtime (x64)：[下载地址](http://www.microsoft.com/en-us/download/confirmation.aspx?id=30679)
2. 必须的PHP配置文件
    * extension_dir = <指向扩展库目录的路径> - extension_dir 需要指向存放 PHP 扩展库文件的目录。可以是绝对路径（如 "C:\PHP\ext"）或相对路径（如 ".\ext"）。在 php.ini 文件中要加载的扩展库都必须在 extension_dir 所指定的目录之中。
    * extension = xxxxx.dll - 对每个需要激活的扩展，都需要一行相应的 "extension=" 语句来说明 PHP 启动时加载 extension_dir 目录下的哪些扩展。
    * log_errors = On - PHP 有错误日志的功能可以将错误报告发送到一个文件中，或者系统服务中（例如系统日志），与下面的 error_log 指令配合工作。在 IIS 下运行时，log_errors 应被激活，并且配合有效的 error_log。
    * error_log = <指向错误日志文件的路径> - error_log 需要指向一个具有绝对或相对路径的文件名用于记录 PHP 的错误日志。Web 服务器需要对此文件有可写权限。最常用的位置是各种临时目录，例如 "C:\inetpub\temp\php-errors.log"。
    * cgi.force_redirect = 0 - 在 IIS 下运行时需要关闭此项指令。这是个在许多其它 web 服务器中都需要激活的目录安全功能，但是在 IIS 下如果激活则会导致 PHP 引擎在 Windows 中出错。
    * cgi.fix_pathinfo = 1 - 此指令可以允许 PHP 遵从 CGI 规则访问真实路径信息。IIS 的 FastCGI 实现需要激活此指令。
    * fastcgi.impersonate = 1 - IIS 下的 FastCGI 支持模拟呼叫用户方安全令牌的能力。这使得 IIS 可以定义请求方的安全上下文。
    * fastcgi.logging = 0 - FastCGI 日志在 IIS 下应被关闭。如果激活，则任何类的任何消息都被 FastCGI 视为错误条件从而导致 IIS 产生 HTTP 500 错误。

配置 IIS 以处理 PHP 请求

1. 切换到服务器管理器界面：win + r -> CompMgmtLauncher
2. 添加CGI服务：角色 -> 添加角色服务 -> CGI
3. 切换到IIS管理器界面：win + r -> inetmgr
4. 添加映射：处理程序映射
    * 请求路径(P)：\*.php
    * 模块(M)：FastCgiModule
    * 可执行文件(可选)(E)：C:\\[Path to PHP installation]\php-cgi.exe
    * 名称(N)：PHP_via_FastCGI
5. 参考文档：[在 IIS 中激活 FastCGI 支持](http://www.php.net/manual/zh/install.windows.iis7.php)

也许还需要

1. 安装URL重写模块：[下载地址](http://www.microsoft.com/zh-cn/download/details.aspx?id=7435)
2. 重启IIS
