---
title: 【MySQL系列】-[1] MySQL8.0数据库软件下载及安装
tags: MySQL
---
MySQL管理软件社区版、企业版、集群版的区别，并以MySQL8.0.20版本进行下载、安装、基本配置做相关示例...
<!-- more -->

## 1、MySQL数据软件的社区版、企业版、集群版区别
- 在这个下载界面会有几个版本的选择。

    （1）. MySQL Community Server 社区版本，开源免费，但不提供官方技术支持。

    （2）. MySQL Enterprise Edition 企业版本，需付费，可以试用30天。
    
    （3）. MySQL Cluster 集群版，开源免费。可将几个MySQL Server封装成一个Server。
    
    （4）. MySQL Cluster CGE 高级集群版，需付费。
    
    （5）. MySQL Workbench（GUI TOOL）一款专为MySQL设计的ER/数据库建模工具。它是著名的数据库设计工具DBDesigner4的继任者。MySQL Workbench又分为两个版本，分别是社区版（MySQL Workbench OSS）、商用版（MySQL Workbench SE）。

- MySQL Community Server 是开源免费的，这也是我们通常用的MySQL的版本。根据不同的操作系统平台细分为多个版本，下面我们以windows平台为例来说明。



## 2、下载MySQL
- 2.1、官网下载地址
  https://dev.mysql.com/downloads/mysql/
- 2.2、选择 MySQL Community Server（社区版）进入下载
- 2.3、选择下载的格式
    - 推荐下载第一个 ZIP Archive 内的软件包，mysql-xxx-win64.zip。（这个文件解压缩后即可使用，是编译好的windows64位MySQL。需要手工配置。）

## 3、安装MySQL
- 3.1、解压下载的压缩包
    - 将压缩包解压到想要将MySQL安装的目录最后的根目录就是最后完整的安装目录
- 3.2、在安装目录中新建 my.ini 空文件并如下配置该文件
  - 打开 ”my.ini“ 文件，复制下列内容，记得替换 【安装目录】 部分，保存
    ```sql
    [mysql]  
    # 设置 mysql 客户端默认字符集  
    default-character-set=utf8  
    ​
    [mysqld]  
    #设置 3306 端口  
    port = 3306  
    ​
    # 设置 mysql 的安装目录  
    basedir= 【安装目录】
    ​
    # 设置 mysql 数据库的数据的存放目录  
    datadir= 【安装目录】\data  
    ​
    # 允许最大连接数  
    max_connections=200  
    ​
    # 服务端使用的字符集默认为 8 比特编码的 latin1 字符集  
    character-set-server=utf8  
    ​
    # 创建新表时将使用的默认存储引擎  
    default-storage-engine=INNODB
    ```
- 3.3、配置环境变量 
  - 鼠标选中我的电脑》
  - 右键选择属性》
  - 选择高级系统设置》
  - 选择高级下的环境变量》
  - 系统环境变量下选择新建》
  - 变量名：`MYSQL_HOME`》
  - 变量值：MySQL安装路径》
  - 编辑系统环境变量下的 `Path` 变量》
  - 在 `Path` 变量下新建环境变量 `%MYSQL_HOME%\bin`
- 3.4、用管理员身份运行命令行工具
  - win+x 选择Windows PowerShell（管理员）/ 命令提示符（管理员）
  - 将命令好工具路径转到MySQL安装目录下的bin目录
    - `cd D:\ASystemResources\ToolsDevelopment\MySQL\mysql-8.0.20-winx64\bin`
  - 输入如下命令建立默认数据库
    ```sql
    mysqld --initialize-insecure --user=mysql 
    ```
    > ① 此时 MySQL 建立了默认的数据库，用户名为 root，密码为空。<br>
    >② 如果提示 mysqld 不存在，检查环境变量设置。

- 3.5、安装服务
    - 输入下列语句，服务安装完成
        ```sql
        mysqld -install
        ```
        >① 第一次安装的话会显示 Service successfully installed.<br>
        >② 已经安装过了，会显示 The service already exists! ...
    - 如未正常安装请先移出服务，输入如下命令
      ```sql
      mysqld -remove
      ```
       >① 移除成功的话会显示 Service successfully removed.
- 3.6、启动服务
  - 输入如下命令启动服务
     ```
    net start mysql 
    ```
    - 如果遇到 MySQL 无法启动，3534，请检查如下：
      - （1）请不要手动创建data目录
      - （2）my.ini文件中配置的目录中是否有t开头的文件夹如果有则在配置路径是使用 `//` 替换
      - （3）my.ini文件的编码方式是不是 `ANSI`格式如果不是请改成这个格式
- 3.7、登录MySQL
  - 输入如下命令回车后输入密码
    ```sql
    mysql -u root -p
    ```
    >① -u 指的是登录的用户名，-p 是密码<br>
    >② 用户名默认为 root，此时密码为空
    
    此时默认密码为空直接回车即可登录
- 3.8、修改密码（第一次登录后应第一时间修改密码）
  - 输入下列语句，将 `password` 替换为新密码，修改密码完成
    ```sql
    ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';
    ```
    >① 为了避免之后出现登录问题，登陆后第一件事情应该是修改密码。<br>
    >② password 是你的新密码部分，自行修改。<br>
    >③ 注意密码在单引号内部 `password`<br>
    >④ 注意结尾的分号 `;`<br>
- 3.9、退出数据库和停止服务
  - 退出数据库
  ```sql
  quit;
  ```
  - 停止数据库服务
  ```sql
  net stop mysql
  ```
参考文章：https://zhuanlan.zhihu.com/p/112765207