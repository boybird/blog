---
title: "解决各种网速慢的问题"
date: "2019-11-02"
---


git http代理

打开 git 配置文件 `vi ~/.gitconfig`

```
[user]
        name = boybird
        email = zxk7516@outlook.com
[http]
[http "https://github.com"]
        proxy = socks5://127.0.0.1:1080
        sslVerify = false
```
