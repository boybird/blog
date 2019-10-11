---
title: "powershell "
date: "2019-10-07"
---


* npm 没有ps1 文件执行权限
    以管理员权限运行 powershell，执行以下命令
    ```ps
    set-executionpolicy remotesigned
    ```