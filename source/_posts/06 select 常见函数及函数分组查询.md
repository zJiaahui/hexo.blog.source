---
title: 【MySQL系列】-[6] SQL常用函数及函数分组查询
tags: 
  - MySQL
---
MySQL中SQL语句常用函数：字符函数、数学函数、日期函数、流程控制函数、分组函数的基本了解、及简单示例，最后学习MySQL中SQL的`SELECT 分组函数,分组列表（要求出现在group by的后面）From 表 WHERE 条件表达式 group by 分组列表 ORDER BY 子句;`分组查询的查询列表由分组函数、分组列表构成；group by 后必须是分组列表...
<!-- more -->
## 常用函数
#### 1、常用函数分类
- 1.1、单行函数
  - 字符函数
  - 数学函数
  - 日期函数
  - 流程控制函数
- 1.2、分组函数

#### 2、单行函数-字符函数
- 2.1、获取参数值的字节个数`length('shdsjka中问12')`
- 2.2、拼接字符串函数 `concat(last_name,'-',first_name)`
- 2.3、大小写转换函数小写转大写 `UPPER('wangwu')` 大转小`LOWER('WANGWU')`
- 2.4、截取字符串 `substr(字符,开始位置,截取个数)`、`substring()`
- 2.5、判断字符在某一段字符里出现的位置找不到返回0`instr('asdfghjk','j')`
- 2.6、去左右空格 `TRIM('  sds   ')`
- 2.7、lpad 用指定字符填充左边至指定的字符长度 `lpad('积分多少快乐',10,'*')`
- 2.8、rpad 用指定字符填充右边至指定的字符长度 `rpad('积分多少快乐',10,'*')`
- 2.9、替换`replace('字符段落','想要替换掉的字符','想要替换成的字符')`

#### 3、单行函数-数学函数
- 3.1、四舍五入 `round(1.55)` `round(1.557,2)`
- 3.2、向上取整`ceil(1.02)`
- 3.3、向下取整`floor(9.99)`
- 3.4、截断`truncate(1.6999,1)`
- 3.5、取余`mod(10,3)`

#### 4、单行函数-日期函数
- 4.1、当前时间加日期 `now()`->2020-10-06 11:22:33
- 4.2、当前日期不包含时间`curdate()`->2020-10-06
- 4.3、当前时间不包含日期`curtime()`->11:22:33
- 4.4、获取指定的部分年、月、日 
`year(now())`->2020,`year('1998-10-1')`->1998

#### 5、流程控制函数
- 5.1、if函数：实现三元运算的效果
  ```SQL
  SELECT IF(表达式1,表达式2,表达式3) 
  # 表达式1结果为true返回表达式2的值为false返回表达式3的值
  ```
   ```SQL
  # 查询员工表中年龄大于50岁的姓名及备注有福利小于50岁的备注无福利
  SELECT `name`,age, IF(age>50,'有福利','无福利') FROM employees;
  ```
- 5.2、case函数
  
  ```sql
  case 要判断的字段或表达式
  when 常量 then 要显示的值或语句;
  when 常量 then 要显示的值或语句;
  ...
  else 要显示的值或语句;
  end
  ```

  ```sql
   # 查询员工工资 
   # 部门号=30的显示工资的1.1倍
   # 部门号=40的显示工资的1.2倍
   # 其他显示原工资

  SELECT salary,id,
  case id
  when 30 then salary*1.1;
  when 40 then salary*1.2;
  else salary;
  end as 倍数工资 from employees;
  ```

    ```sql
  case 
  when 条件 then 要显示的值或语句;
  when 条件 then 要显示的值或语句;
  ...
  else 要显示的值或语句;
  end
  ```
  ```sql
   # 查询员工工资 
   # 部门号>30的显示工资的1.1倍
   # 部门号>40的显示工资的1.2倍
   # 其他显示原工资
  SELECT salary,id,
  case 
  when id>30 then salary*1.1;
  when id>40 then salary*1.2;
  else salary;
  end as 倍数工资 from employees;
  ```

#### 6、分组函数
- sum 求和 处理数值类型
- avg 平均值 处理数值类型
- max 最大值 处理任何类型
- min 最小值 处理任何类型
- count 计算个数 处理任何类型

```sql
# 求员工表所有员工工资和
SELECT SUM(salary) FROM employees;
SELECT SUM(DISTINCT salary) FROM employees; #去重

# 求员工表所有员工工资的平均值
SELECT AVG(salary) FROM employees;
SELECT AVG(DISTINCT salary) FROM employees; #去重

# 求员工表所有员工工资的最高工资
SELECT MAX(salary) FROM employees;
SELECT MAX(DISTINCT salary) FROM employees; #去重

# 求员工表所有员工工资的最低工资
SELECT MIN(salary) FROM employees;
SELECT MIN(DISTINCT salary) FROM employees; #去重

# 求员工表有多少条salary字段数据
SELECT count(salary) FROM employees;
SELECT count(DISTINCT salary) FROM employees; #去重
```
#### count统计表中数据行数

```sql
#统计表中数据行数
SELECT count(*) FROM employees;
SELECT count(1) FROM employees;

```
## 分组函数查询

**【语法】**
```sql
SELECT 分组函数,分组列表（要求出现在group by的后面）
From 表
WHERE 条件表达式
group by 分组列表
ORDER BY 子句;

# 【注意 】和分组函数一同查询的字段必须是 group by 后的字段
```
**【案例】**
```sql
按单字段分组查询
# 查询每个工种的最高工资（以不同工种id为分组要求，查询各工种分组中最高工资）
SELECT MAX(salary) ,job_id FROM employees group by job_id;

#查询邮箱中包含a字符的每个部门的平均工资
SELECT AVG(salary),department_id FROM employees WHERE email LIKE '%a' GROUP BY department_id;

#查询有奖金的每个领导手下员工的最高工资
SELECT MAX(salary),manager_id FROM employees WHERE commission_pct IS NOT NULL GROUP BY manager_id;

按多字段分组查询
#查询每个部门每个工种的员工平均工资
SELECT AVG(salary),department_id,job_id FROM employees GROUP BY department_id,job_id;

#查询每个部门每个工种的员工平均工资,并从高到低显示
SELECT AVG(salary),department_id,job_id FROM employees GROUP BY department_id,job_id ORDER BY AVG(salary) DESC;
```

     

