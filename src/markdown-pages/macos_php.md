---
title: "macos lnmp 环境"
date: "2019-09-19"
---


# 环境安装
## php + php-fpm
```sh
brew install php@5.6
brew services start php@5.6 # 或者
/usr/local/Cellar/php@5.6/5.6.30/sbin/php-fpm --fpm-config /usr/local/etc/php/5.6/php-fpm.conf
```
## nginx
```sh
brew install nginx
```
## php 拓展安装, redis为例
  * php >= 7.0 
  ```sh
  /usr/local/Cellar/php@7.0/7.0.0/bin/pecl install redis
  ```

  * php < 7.0 
  ```sh
  /usr/local/Cellar/php@7.0/7.0.0/bin/pecl install https://pecl.php.net/get/redis-2.2.8.tgz
  ```


