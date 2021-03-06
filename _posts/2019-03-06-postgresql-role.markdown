---
title: postgresql命令创建只读用户
layout: post
date: '2019-03-06 11:05:25'
categories: postgresql
---

# 第一种方法：
1.创建一个用户名为readonly密码为123456的用户
```
CREATE USER readonly WITH ENCRYPTED PASSWORD '123456';
```

2.更新用户默认为只读事务
```
  alter user readonly set default_transaction_read_only=on;
```

3.把所有库的public的USAGE权限给到readonly
```
  GRANT USAGE ON SCHEMA public to readonly;      
```

4.授予select权限(要进入到具体数据库操作在哪个db环境下执行就授予那个db的权限)
```
   grant select on all tables in schema public to readonly;
```

# 第二种方法：

1、创建只读角色
```
CREATE ROLE readaccess;
```
2、授予对现有表的访问权限
```
GRANT USAGE ON SCHEMA public TO readaccess;
GRANT SELECT ON ALL TABLES IN SCHEMA public TO readaccess;
```
3、授予后面新增表的访问权限
```
ALTER DEFAULT PRIVILEGES IN SCHEMA public GRANT SELECT ON TABLES TO readaccess;
```
4、创建用户
```
CREATE USER testuser WITH PASSWORD 'mypassword';
GRANT readaccess TO testuser;
```