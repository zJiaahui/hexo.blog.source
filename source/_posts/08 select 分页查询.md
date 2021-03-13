---
title: 【MySQL系列】-[8] select分页查询
tags: 
  - MySQL
---
当查询出来的数据很多时,网站页面一页无法展示全，并且当查询某一条件下的数据有几千上万条时，是没有必要一次将所有的数据都查询出来的，因此可以用到分页查询，一次只查询固定的条数，跳到下一页时就从这一页最后一条的下一条开始查询同样的固定条数...
<!-- more -->
**【语法】**
```SQL
SELECT 查询列表 FROM 表名 WHERE 条件表达式 LIMIT 要从第几条开始查的索引(索引是从0开始记),查询多少条;
```
**【示例】**
  ```SQL
  #查询员工表中前5条数据
  SELECT * FROM employees LIMIT 0,5;

  #查询员工表第11条-25条的数据
  SELECT * FROM employees LIMIT 10,15;

  #查询员工表中有奖金的员工信息，并且工资较高的前10名数据
  SELECT * FROM employees WHERE salary IS NOT NULL ORDER BY salary DESC LIMIT 10;
  ```

**【注意】**
- limit语句放在查询语句的最后

**【分页查询公式】**
```sql
当前要显示的页数page，每页要显示的条数size
SELECT 查询列表 FROM 表名 WHERE 条件表达式 LIMIT (page-1)*size,size;
```
