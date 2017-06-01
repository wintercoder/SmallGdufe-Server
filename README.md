# 移动广财服务端-安装指南

**非开源 ** 

requirements: PHP >= 5.4.0  Redis >= 3.x

如果你PHP是5.3的，可参考 [此文](https://www.zerostopbits.com/how-to-install-upgrade-php-5-3-to-php-5-5-on-centos-6-7/) 更新版本到5.5

## 安装redis
1. 源码安装redis https://redis.io/download ，建议3.x
2. 关闭保护模式 protected mode  
   修改redis源码安装目录下的redis.conf，如下修改参数

   		daemonize yes
   		protected-mode no

  如需知道具体意义可参考 [网上博文](http://www.cnblogs.com/zhoujinyi/p/5565647.html)

2. 运行redis，在redis目录下 ： 
   ​
   ​	redis-server redis.conf

## 配置数据库

安装数据库就不说了，装完修改 `config/db.php` 的配置

## 解决代码库依赖
- 建议直接使用整个代码目录，含vendor目录，这样就不用安装composer了。
- 如果只使用代码目录，不使用原有库，则需要
  1. [安装composer](http://docs.phpcomposer.com/00-intro.html#Installation-Windows) ，下载安装包安装的时候是在线安装，需要科学上网。
  2. 安装完之后，执行 `composer config -g repo.packagist composer https://packagist.phpcomposer.com` 命令开启全局composer镜像，否则安装库依赖超级慢。
  3. 在项目目录下执行 `composer install` 安装各种依赖库。

## 运行
在已经跑了redis和修改数据库后，在项目目录下  

    php yii serve www.wintercoder.com:82

或者自己配置 apache/nginx 去跑也行。注意：**yii自带的为单线程模式，如果更新APP的地址也在yii里会卡住全部用户，故勿用于生产环境**

## 更新Api文档
Api文档是用Apidoc生成的，需要NodeJs环境。
1. 安装NodeJs： http://www.runoob.com/nodejs/nodejs-install-setup.html

2. 解决国内npm命令安装依赖速度慢的问题：

   npm config set registry http://registry.npm.taobao.org

3. 修改完 `controller/` 的注释就在项目根目录就可以生成到 `apidoc` 目录下

   apidoc -i controllers/ -o apidoc/