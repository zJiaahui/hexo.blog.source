---
title: 【MySQL系列】-[4] SQL查询-条件查询
tags: MySQL
---
MySQL中SQL语句中条件查询的基本语法`SELECT 查询列表 FROM 表名 WHERE 条件表达式;`讲解，以及对语法中条件表达式中的：条件运算符表达式  ` > 、 <、  =、  != 、 >=  、 <= `、逻辑运算功符表达式  `&&、  || 、!、  and 、 or 、 not`（符号和英文是对应的推荐用英文）、模糊条件表达式  ` like 、  between and 、in  、 is null`几种情况进行示例...
<!-- more -->
## 1、条件查询语法及示例
- ### **【语法】**
```SQL
SELECT 查询列表 FROM 表名 WHERE 条件表达式;
```
>注释》
>
> 条件表达式：<br>（1）条件运算符表达式  ` > 、 <、  =、  != 、 >=  、 <= `<br>（2）逻辑运算功符表达式  `&&、  || 、!、  and 、 or 、 not`（符号和英文是对应的推荐用英文） <br>（3）模糊条件表达式  ` like 、  between and 、in  、 is null`


- ### **【示例】` > 、 <、  =、  != 、 >=  、 <= `**
```SQL
1-0、查询员工表中年龄大于35岁的所有员工信息
SELECT * FROM employees WHERE age>35;

1-1、查询员工表中年龄小于25岁的所有员工信息
SELECT * FROM employees WHERE age<25;

1-2、查询员工表中年龄不等于20岁的所有员工信息
SELECT * FROM employees WHERE age != 20;

1-3、查询员工表中年龄小于等于20岁的所有员工信息
SELECT * FROM employees WHERE age <= 20;

1-4、查询员工表中年龄大于等于20岁的所有员工信息
SELECT * FROM employees WHERE age >= 20;
```

- ### **【示例】` and 、 or 、 not `**

    ```SQL
    1-0、查询员工表中年龄大于35岁小于40岁的所有员工信息
    SELECT * FROM employees WHERE age>35 AND age<40;

    1-1、查询员工表中年龄不在35-40之间或者大于50岁的所有员工信息
    SELECT * FROM employees WHERE NOT(age>35 AND age<40) OR age>50;
    ```
- ### **【示例】`like 、  between and 、in  、 is null`**

    ```SQL
    1-0、查询员工表中名字中包含a的所有员工信息
    SELECT * FROM employees WHERE `name` LIKE '%a%';
    # %表示无数个通配占位符（%a%表示a的前后可以有无数个其他字符a后面也是） 

    1-1、查询员工表中名字中第二个字母为a的所有员工信息
    SELECT * FROM employees WHERE `name` LIKE '_a%';
    # _ 表示一个通配占位符（_a% 表示的是第一个随便是什么字符第二个是a字符后面%是表示未知个数占位通配符）
    #当要查询的就是_本身的话则可通过\_进行转义

    1-2、查询员工表中年龄大于35岁小于40岁的所有员工信息
    SELECT * FROM employees WHERE age BETWEEN 35 AND 40;
    #包含临界值35和40

    1-3、查询员工表中名字是张三、李四和王五的所有员工信息
    SELECT * FROM employees WHERE `name` in ('张三','李四','王五');
    # 比使用OR的语法简介精炼

    1-4、查询员工表中没有登记年龄的员工名字
    SELECT `name` FROM employees WHERE age IS NULL;
    #SQL中不支持age=NULL这种判断

    1-5、查询员工表中有登记年龄的员工名字
    SELECT `name` FROM employees WHERE age IS NOT NULL;
    ```

    查询员工编号为152的员工姓名和部门编号和年薪
    ```sql
    SELECT `name`,department_id,salary*12*(1+IFNULL(commission_pct,0)) AS `年薪` FROM employees WHERE employee_id=152;
    ```

     

