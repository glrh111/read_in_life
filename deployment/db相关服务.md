# 数据库相关服务部署

* 注意将数据库的数据卷挂载在host上.不然container挂掉, 服务就不见了.

## Postgresql

### 概述

1. Postgres功能强大, 支持类型丰富

### 部署流程

```
1. docker pull postgres
2. docker run --name postgres -e POSTGRES_PASSWORD=wocao -v /home/glrh11/pgdata:/var/lib/postgresql/data -d postgres
3. docker exec -it postgres bash
4. 初始化数据库 数据库名称 read_in_life 密码 wocao 

adduser read_in_life  # 新建用户
su - postgres         # 切换用户
psql                  # 进入DBMS

CREATE USER read_in_life WITH PASSWORD 'wocao'; # 创建数据库角色
CREATE DATABASE read_in_life OWNER read_in_life; # 创建app专属数据库
GRANT ALL PRIVILEGES ON DATABASE read_in_life to read_in_life; # 授全权
```

## Redis

### 概述

Redis功能强大.艹

### 部署流程

```
1. docker pull redis
2. docker run --name redis -v /home/glrh11/redisdata/:/data/ -d redis redis-server --appendonly yes
```



