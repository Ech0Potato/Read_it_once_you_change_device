# Read_it_once_you_change_device

当电脑更换为新的之后，当前电脑换新的时候做的一些配置容易忘掉，这里记录一下常处理的一些问题。

# TIM or QQ 轻聊版转移安装目录无法成功问题
默认 TIM or QQ 所在的位置是我的文档，而我的文档位于 C 盘，长期占用空间较大，因此需要转移默认用户文件夹所在位置。

按照 TIM 内部的功能进行转移，重新启动后发现 TIM 依然使用默认的文件夹，即位于我的文档中的文件夹。

这个 bug 直到 2021年9月12日也没有修复：

解决方案：https://blog.csdn.net/VimGuy/article/details/104666360

# 配置 git 的代理

全盘寻找 .gitconfig 文件，一般位于当前用户的根目录下面。

添加字段：
```ini
[ssh]
       proxy = socks5://127.0.0.1:7890
[http]
       proxy = http://127.0.0.1:7890
[https]
       proxy = https://127.0.0.1:7890
```

也可以参照下面的配置方式，为 github.com 这个 Host 专门配置 SSH 代理。

如果说使用的代理软件（代理服务器）具备根据域名和ip的分流功能，那么推荐使用上方提到的配置方式。

但如果不具备分流功能，且仅想代理 github.com 或者特定的 SSH 协议，那么使用如下的配置方案：

Link1: https://kaige.org/2020/02/11/proxy-setting-for-git-on-Windows/ 
Link2: https://gist.github.com/laispace/666dd7b27e9116faece6#gistcomment-2652557

即：

**Mac OS 平台**

因为 Mac OS 为 Unix-like 系统，所以具备 nc 程序。

```gitconfig
Host github.com
    User git
    ProxyCommand nc -v -x 127.0.0.1:1086 %h %p
    
```

**Windows 平台**

因为 Windows 的 git minGW 不具备 nc 程序，因此使用 connect 代替。

```gitconfig
Host github.com
     User git
     ProxyCommand connect -S 127.0.0.1:1086 %h %p
```
