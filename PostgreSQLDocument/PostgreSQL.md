[TOC]

# Docker安装PostgreSQL

https://blog.csdn.net/Rong_Toa/article/details/88917424

```shell
docker pull postgres:12.4

docker run --name postgres -e POSTGRES_PASSWORD=123456 -e TZ=PRC -p 5432:5432 -v/data/docker/pg/data:/var/lib/postgresql/data -d postgres:12.4 

run：创建并运行一个容器； –name：指定创建的容器的名字； -e POSTGRES_PASSWORD=password，设置环境变量，指定数据库的登录口令为password； -p 54321:5432，端口映射将容器的5432端口映射到外部机器的5432端口; -d postgres:12.4，指定使用postgres:12.4作为镜像;
-e TZ=PRC 时区-中国
-v来指定把postgres的数据目录 /data/docker/pg/data:/var/lib/postgresql/data 映射到/data/docker/pg/data里面
注意： postgres镜像默认的用户名为postgres，登陆口令为创建容器是指定的值。

docker ps 

-- 查看 postgres 详细信息
docker inspect postgres 

-- 进入容器,以管理员权限进入
docker exec -u 0  -it  22ab1619682d  /bin/bash

cd  /var/lib/postgresql/data
修改pg_hba.conf文件,添加
host all all 0.0.0.0/0 md5

修改postgresql.conf文件，添加
listen_addresses = ’*’

-- 连接Postgresql
psql -h 172.16.35.179 -U postgres -d postgres

-- 创建用户
CREATE USER dbuser WITH PASSWORD '*****';

-- 创建用户数据库，这里为exampledb，并指定所有者为dbuser。
CREATE DATABASE exampledb OWNER dbuser;

-- 将exampledb数据库的所有权限都赋予dbuser：
GRANT ALL PRIVILEGES ON DATABASE exampledb TO dbuser;

```

控制台还提供一系列其他命令。

> - \h：查看SQL命令的解释，比如\h select。
> - \?：查看psql命令列表。
> - \l：列出所有数据库。
> - \c [database_name]：连接其他数据库。
> - \d：列出当前数据库的所有表格。
> - \d [table_name]：列出某一张表格的结构。
> - \du：列出所有用户。
> - \e：打开文本编辑器。
> - \conninfo：列出当前数据库和连接的信息。

# 一些教程

http://www.postgres.cn/docs/13/

https://www.lidihuo.com/postgresql/postgresql-json.html

https://www.yiibai.com/postgresql/

https://github.com/postgres-cn/pgdoc-cn

https://pg.sjk66.com/index.html
