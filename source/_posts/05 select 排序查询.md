---
title: 【MySQL系列】-[5] SQL查询-排序查询
tags: MySQL
---
MySQL中SQL语句的排序查询语法`SELECT 字段 FROM 表 WHERE 条件 ORDER BY 排序字段 ASC/[DESC];`讲解以及对升序查询、降序查询的相关示例...
<!-- more -->
## 1、排序查询语法及示例
**【语法】**
```sql
#从低到高
SELECT 字段 FROM 表 WHERE 条件 ORDER BY 排序字段 ASC;

#从高到低
SELECT 字段 FROM 表 WHERE 条件 ORDER BY 排序字段 DESC;
```
>排序字段可以是别名、函数、多个字段排序、表达式 

**【示例】**
```sql
1-0、查询员工信息，要求按年龄从大到小排列
SELECT * FROM employees ORDER BY age DESC;

1-1、查询员工信息，要求按年龄从小到大排列
SELECT * FROM employees ORDER BY age ASC;
```


     

