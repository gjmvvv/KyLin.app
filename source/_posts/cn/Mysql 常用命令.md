---
title: Mysql 常用命令
iscopyright: true
comments: true
lang: cn
tags:
  - mysql
  - command
categories:
  - mysql
abbrlink: mysql
date: 2019-08-11 16:45:21
---


## SQL命令的使用规则

1、每条SQL命令必须以 ; 结尾
2、SQL命令不区分字母大小写
3、使用 \c 来终止当前命令的执行

- 登录
    ```
        $ mysql -u用户名 -p
    ```


### 库相关

- 查看当前所在库
    ```
        $ select database(); 
    ```
    
- 查看所有库
    ```
        $ show datatables; 	
    ```

- 切换库
    ```
        $ use 库名称;
    ``` 

- 创建库
    ```
        $ create database gp_dev default charset=utf8;
    ```


### 表相关 

- 查看所有数据
    ```
        $ select * from 表名称
    ``` 

- 查看指定列 表中所有数据 
    ```
        $ select 列名称(逗号区分) from 表名称
    ``` 

- 查看表结构
    ```
        $ desc 表名称
    ``` 

 
## 用户相关
- 查看用户
    ```
    mysql> select host,user,authentication_string from mysql.user;
    ```

- 创建用户
    ```
    mysql> create user "username"@"localhost" identified by "password";
    ```
    > host="localhost"为本地登录用户，host="ip"为ip地址登录，host="%"，为外网ip登录

    - e.g.
        ```
        mysql> create user 'test'@'localhost' identified by '123';
        mysql>create user 'test'@'192.168.7.22' identified by '123';
        mysql>create user 'test'@'%' identified by '123';
        ```

 
- 删除用户
    ```
    mysql> drop user 'username'@'host';
    ```


- 授权
    ```
    mysql> grant privileges on databasename.tablename to 'username'@'host' IDENTIFIED BY 'PASSWORD';
    ```
    > privileages: all priveleges 或 多个 update select等 逗号分隔 <br>
    > on: 指定权限 库和表 \*.* == 据库名.表名 <br>
    > IDENTIFIED 指定密码 可以省略 <br>
    
    - e.g.
        ```
        授予用户通过外网IP对于该数据库的全部权限
        mysql> grant all privileges on `test`.* to 'test'@'%' ;

        授予用户在本地服务器对该数据库的全部权限
        mysql> grant all privileges on `test`.* to 'test'@'localhost';   
        
        添加查询权限
        mysql> grant select on test.* to 'test'@'localhost';  
        
        给予插入权限
        mysql> grant insert on test.* to 'test'@'localhost';

        添加删除权限
        mysql> grant delete on test.* to 'test'@'localhost'; 

        添加更新权限
        mysql> grant update on test.* to 'test'@'localhost';

        刷新权限
        mysql> flush privileges;
        ``` 
         

- 查看权限
    ```
    查看所有用户权限
    mysql> show grants;
    
    查看某个用户权限
    mysql> show grants for 'username'@'host';
    ```
     

- 删除权限
    ```
    mysql> revoke privileges on databasename.tablename from 'username'@'host';
    ```
    -e.g.
        ```
        revoke delete on test.* from 'test'@'localhost';
        ```

- 更改用户名
    ```
    mysql> rename user 'test'@'%' to 'test2'@'%';
    ```

- 更改密码
    ```
    mysql> SET PASSWORD FOR 'test'@'localhost' = PASSWORD('123456');
    ```


## 问题解决方案
- Q: pycharm中python3.6+pymysql+mysql8.0.1连接报错
    1. 命令行连接 mysql -uroot -p123456
    2. ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '123456';
