---
title: 【MySQL系列】-[2] MySQL SQL语法命令
tags: MySQL
---
MySQL中SQL语句的语法命名规范、注释以及启动/关闭MySQL服务、登录MySQL、查看MySQL中的数据库（查看指定数据库的表及表结构）、MySQL版本等常用命令...
<!-- more -->
## 1、规范
```
1-0、不区分大小写（关键字大写、表名、列名等小写）
1-1、命令使用分号结尾
1-2、命令可以自行缩进或换行（建议关键字单独一行）
```

## 2、注释
- 单行注释
    - 2-0、`#注释文字`
    - 2-1、`-- 注释文字`
- 多行注释
    - 2-3、`\* 注释文字 \*`

## 3、常用命令

- 3-0、启动和关闭MySQL服务
  
    **【语法】**
    ```sql
    # 语法
    net start 服务名称

    net stop 服务名称
    ```
    **【示例】**
    ```sql
    # 启动MySQL服务（打开管理员权限的命令行工具输入如下命令）
    net start myql

    # 关闭MySQL服务（打开管理员权限的命令行工具输入如下命令）
    net stop mysql
    ```
- 3-1、登录数据库（MySQL服务开启的状态下才能登录数据库）
    
    **【语法】**

     ```sql
     # 完整语法
     mysql -h 主机名 -P 端口号 -u 用户名 -p 回车输入密码再回车登录

     #简易语法
     mysql -u 用户名 -p 回车输入密码再回车登录
     ```
     **【示例】**
     ```sql
     mysql -u root -p 回车输入密码再回车登录
     ```
    ```sql
     mysql -h localhost -P 3306 -u root -p 回车输入密码再回车登录
     ```

     
- 3-2、查看mysql中的所有数据库
   ```sql
   show databases;
   ```
   > Mysql会有默认的四个数据库用来保存元数据信息、用户信息、性能信息、测试数据库
- 3-3、选择需要操作的数据库比如选择test数据库
    ```sql
    use test;
    ```
- 3-4、查看该数据库中的所有数据表
    ```sql
    show tables;
    ``` 
- 3-5、查看某个表的表结构
    
    ```sql
    desc 表名称;
    ```
- 3-6、查看当前选中的是那个数据库
    
    ```sql
    select database();
    ``` 

- 3-7、查看MySQL版本
    - (1) 登录MySQL状态
        
        ```sql
        select version();
        ```
    - (2)未登录状态
       
        ```sql
        mysql --version
        ```
        ```sql
        mysql -v
        ```