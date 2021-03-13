---
title: Node.js Mysql8客户端不支持认证协议引发的“ER_NOT_SUPPORTED_AUTH_MODE”问题
tags:
    - MySQL
    - Nodejs
---

## 1.当我们再Nodejs中连接Mysql8时出现如下错误信息
```
Client does not support authentication protocol requested by server; consider upgrading MySQL client
```
## 2.原因

导致这个错误的原因是，目前，最新的mysql模块并未完全支持MySQL 8的“caching_sha2_password”加密方式，而“caching_sha2_password”在MySQL 8中是默认的加密方式。因此，下面的方式命令是默认已经使用了“caching_sha2_password”加密方式，该账号、密码无法在mysql模块中使用。

## 3.解决办法

解决方法是从新修改用户root的密码，并指定mysql模块能够支持的加密方式：“mysql_native_password”加密方式。这种方式是在mysql模块能够支持。

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '你的新密码';

```