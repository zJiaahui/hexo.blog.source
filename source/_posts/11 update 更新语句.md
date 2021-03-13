---
title: 【MySQL系列】-[11] update 更新语句
tags:
    - MySQL
---
SQL更新语句`update 表名 set 要更新的列名=新值,要更新的列名=新值,... where 条件表达式 ;`
<!-- more -->
**【更新语句-语法】**
```SQL 
#单表

update 表名 set 要更新的列名=新值,要更新的列名=新值,... where 条件表达式 ;

```
```SQL
#多表

update 表1名,表2名 set 表1名.要更新的列名=新值,表2名.要更新的列名=新值,... where 条件表达式 ;

```