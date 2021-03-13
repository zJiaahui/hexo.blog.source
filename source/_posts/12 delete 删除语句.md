---
title: 【MySQL系列】-[12] delete 删除语句
tags:
    - MySQL
---
SQL删除语句`delete from 表名 where 条件表达式 ;`
<!-- more -->
**【更新语句-语法】**
```SQL 
delete from 表名 where 条件表达式 ;

```
```SQL
# 删除手机号以8结尾的员工信息
DELETE FROM employees WHERE phone LIKE '%8';
```