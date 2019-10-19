---
title: "Vim(nvim) 配置教程"
date: "2019-10-19"
---

### 配置

nvim 配置文件不是配置的 ~/.vimrc, 在linux 操作系统上一般是 .config/nvim/init.vim 但是windows 上的目录比较难找，以便下面的创建并编辑 nim 配置文件
```
:call mkdir(stdpath('config'), 'p')
:exe 'edit '.stdpath('config').'/init.vim'
```

### 插件


### 键位
