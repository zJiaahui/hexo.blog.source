---
title: 【MySQL系列】-[3] SQL查询-基础查询
tags: 
    - MySQL
---
MySQL中SQL查询中的基础查询语法`SELECT 查询列表 FROM 表名;`以及对语法中查询列表字段（表字段、常量、表达式、函数）的示例...
<!-- more -->
## 1、基础查询语法及示例
- ### **【语法】**
```SQL
SELECT 查询列表 FROM 表名;
```
>  **注释》**    
>（1）查询列表可以是表字段、常量、表达式、函数（有时候每个字段需要添加着重符号\` \` 用于区分为非关键字）<br>
>（2）查询的结果会形成一个新的虚拟表，该虚拟表的字段就是查询语句的查询列表名称 


- ### **【示例】**
- #### **1.2、字段查询示例**
```SQL
# 1-1、查询员工表中的姓名字段
SELECT `name` FROM employee;

# 1-2、查看员工表的中所有人的姓名和年龄
SELECT `name`,`age` FROM employee;

# 1-3、查询员工表中所有人的所有信息
SELECT * FROM employee;
```
- #### **1.3、常量查询示例**
```SQL
SELECT  100 FROM employee;

SELECT 'john' FROM employee;
```
- #### **1.4、表达式查询示例**
```SQL
SELECT  10+20 FROM employee;
```
>**注释 》**   
>sql中的加号+只是运算符,有一个不为数字则将其转换为数值再做加法，如果转换失败则将其用0代替再做加法运算,有一个为null结果为null

    ```SQL
    SELECT 100%98 FROM employee;
    ```
- #### **1.5、函数查询示例**
```SQL
SELECT version() FROM employee;
```

## 2、起别名

- ### **【语法】**
```SQL
SELECT 字段1 AS 字段1别名, 字段2 AS 字段2别名 FROM 表名；
```
>  **注释》**    
>（1）查询的结果会形成一个新的虚拟表，该虚拟表的字段就是查询语句的查询列表名称的别名<br>
>  (2) 不是每一项都需要同时取别名

## 3、结果去重

- ### **【语法】**

```SQL
SELECT DISTINCT 字段 FROM 表名;
```
>  **注释 》**    
>（1）查询的结果会形成一个新的虚拟表，去掉结果中重复的内容
> (2) 只能有一个查询字段的时候使用

## 4、查询两个字段合成一个字段显示结果

- ### **【语法】**

```SQL
SELECT CONCAT(字段1,字段2) AS 别名 FROM 表名;
```
- ### **【示例】**

```SQL
4-0、查询员工表的中所有员工的姓和名并合并成完整的姓名输出(不要使用单引号包括字段名)
SELECT CONCAT(fristname,lastname) AS name FROM employee;
```
