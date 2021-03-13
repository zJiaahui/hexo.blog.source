---
title: Git修改和配置本地用户名和邮箱
tags:
    - Git
---

查看所有配置
```
git config --list
```
查看user.name/user.email
```
 git config user.name
 git config user.email
```
配置user.name/user.email
```
 git config user.name " "
 git config user.email " "
```

修改已经配置过的user.name或email
```
git config --global --replace-all user.name "name"
git config --global --replace-all user.email "email"
```