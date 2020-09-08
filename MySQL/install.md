# MySQL 学习笔记

## 1. 安装

[官网](https://dev.mysql.com/downloads/)

### 1.1 Windows

[windows terminal](https://www.zhihu.com/question/353701331) sudo 管理员权限

```bash
@echo off
mode con lines=30 cols=60
%1 mshta vbscript:CreateObject("Shell.Application").ShellExecute("cmd.exe","/c %~s0 ::","","runas",1)(window.close)&&exit
cd /d "%~dp0"
start C:\Users\yunyi\AppData\Local\Microsoft\WindowsApps\wt.exe
```

```ini
[mysqld]
# 设置3306端口
port=3306
# 设置mysql的安装目录
basedir=E:\\mysql-5.7.22-winx64
# 设置mysql数据库的数据的存放目录
datadir=E:\\mysql-5.7.22-winx64\\data
# 允许最大连接数
max_connections=200
# 允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
# 服务端使用的字符集默认为UTF8
character-set-server=utf8
# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
[client]
# 设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8
```

忘了密码

```bash
# 会产生一个随机密码
mysqld --initialize --user=mysql --console 
mysqld -install
net start MySQL
mysql -u root -p
ALTER USER root@localhost IDENTIFIED  BY '123456';
exit
mysql -u root -p
```

```bash
net stop mysql
```

### 2. SQL语句

```bash
show databases;
create database test;
use test;
show tables;
```

创建数据表

```bash
CREATE TABLE pet (
    name VARCHAR(20),
    owner VARCHAR(20),
    species VARCHAR(20),
    sex CHAR(1),
    birth DATE,
    death DATE);
show tables;
describe pet;
desc pet;
```

字段、记录

```bash
+---------+-------------+------+-----+---------+-------+
| Field   | Type        | Null | Key | Default | Extra |
+---------+-------------+------+-----+---------+-------+
| name    | varchar(20) | YES  |     | NULL    |       |
| owner   | varchar(20) | YES  |     | NULL    |       |
| species | varchar(20) | YES  |     | NULL    |       |
| sex     | char(1)     | YES  |     | NULL    |       |
| birth   | date        | YES  |     | NULL    |       |
| death   | date        | YES  |     | NULL    |       |
+---------+-------------+------+-----+---------+-------+
```

查看表中的记录

```bash
selet * form pet;
```

如何添加记录

```bash
INSERT INTO pet
VALUES ('Ruffball','Dinae','hamster','f','1999-03-30',NULL);
insert into pet
values ('Ruffball','Dinae','hamster','f','1999-03-30',NULL);
```

常用数据类型：

数值、日期、字符串

TINYINT  
SMALLINT  
MEDIUMINT  
INT INTERGER  
BIGINT  
FLOAT  
DOUBLE  
DECIMAL  

```bash
create table testtype (number TINYINT);
insert into testtype values(128);
insert into testtype values(128);
```

增加，删除，查 改。

```bash
insert into pet values ('David','Dinae','hamster','f','1999-03-30',NULL);
delete from pet where name='David';
update pet set name='DD' where owner='Dinae';
```

约束种类：

+ 主键约束
  + (`primary key`)：唯一确定一张表的一个记录。通过某个字段添加字段。使得该字段不重复且不为空。

    ```bash
    create table user(
        id int primary key,
        name varchar(20)
    );
    Query OK, 0 rows affected (0.10 sec)
    ```

    ```bash
    mysql> desc user;
    +-------+-------------+------+-----+---------+-------+
    | Field | Type        | Null | Key | Default | Extra |
    +-------+-------------+------+-----+---------+-------+
    | id    | int         | NO   | PRI | NULL    |       |
    | name  | varchar(20) | YES  |     | NULL    |       |
    +-------+-------------+------+-----+---------+-------+
    2 rows in set (0.00 sec)
    ```

    ```bash
    insert into user values(1,'张三');
    mysql> insert into user values(1,'张三');
    ERROR 1062 (23000): Duplicate entry '1' for key 'user.PRIMARY'
    mysql> insert into user values(2,'张三');
    Query OK, 1 row affected (0.04 sec)
    mysql> insert into user values(NULL,'张三');
    ERROR 1048 (23000): Column 'id' cannot be null
    ```

  + 联合主键：

    ```sql
    create table user2(
        id int,
        name varchar(20),
        passward varchar(20),
        primary key(id,name)
    );
    ```

    ```bash
    insert into user2 values(1,'张三','123');
    insert into user2 values(1,'张三','123'); # error
    insert into user2 values(2,'张三','123');
    insert into user2 values(NULL,'张三','123'); # error
    ```

+ 自增约束：

    ```sql
    create table user3(
        id int primary key auto_increment,
        name varchar(20)
    );
    insert into user3 (name) values ('张三');
    insert into user3 (name) values ('张三');
    ```

    ```bash
    mysql> select * from user3;
    +----+------+
    | id | name |
    +----+------+
    |  1 | 张三 |
    |  2 | 张三 |
    +----+------+
    2 rows in set (0.00 sec)

    mysql> desc user3;
    +-------+-------------+------+-----+---------+----------------+
    | Field | Type        | Null | Key | Default | Extra          |
    +-------+-------------+------+-----+---------+----------------+
    | id    | int         | NO   | PRI | NULL    | auto_increment |
    | name  | varchar(20) | YES  |     | NULL    |                |
    +-------+-------------+------+-----+---------+----------------+
    2 rows in set (0.00 sec)
    ```

    ```sql
    create table user3(
        id int,
        name varchar(20)
    );
    alter table user4 add primary key(id);
    alter table user4 drop primary key;
    alter table usr4 modify id int primary key;
    ```

+ 唯一约束:约束修饰的字段的值不能重复,可以为空，主键不能为空
  
    ```sql
    create table user5(
        id int,
        name varchar(20)
    );
    alter table user5 add unique(name);
    ```

    ```bash
    mysql> desc user5;
    +-------+-------------+------+-----+---------+-------+
    | Field | Type        | Null | Key | Default | Extra |
    +-------+-------------+------+-----+---------+-------+
    | id    | int         | YES  |     | NULL    |       |
    | name  | varchar(20) | YES  | UNI | NULL    |       |
    +-------+-------------+------+-----+---------+-------+
    2 rows in set (0.00 sec)
    ```

    ```sql
    insert into user5 values(1,'张三');
    insert into user5 values(1,'张三'); # ERROR 1062 (23000): Duplicate entry '张三' for key 'user5.name'
    insert into user5 values(1,'李四'); # OK.
    ```

    ```sql
    create table user8(
        id int,
        name varchar(20),
        unique(name,id) # 可以写多个
    );
    create table user7(
        id int,
        name varchar(20) unique
    );
    ```

    删除唯一约束

    ```sql
    alter table user7 drop index name;
    alter table user7 modeify varchar(20) unique;
    ```

    小结:
    1. 建表的时候添加
    2. alter ... add ...
    3. alter ... modify ...
    4. 删除 alter ... drop ...

+ 非空约束:修饰的字段不能为空

    ```sql
    create table user9(
        id int,
        name varchar(20) not null
    );
    insert into user9 (id) values (1); # ERROR
    insert into user9 values(1,'张三');
    insert into user9 values('李四');
    ```

+ 默认约束：没有传值就使用默认值，传了就不使用。

    ```sql
    create table user10(
        id int,
        name varchar(20),
        age int default 10
    );
    insert into user10 (id,name) values (1,'张三');
    ```

+ 外键约束：涉及到两个表：主表和副表 附表子表

    ```sql
    create table classes(
        id int primary key,
        name varchar(20)
    );
    create table students(
        id int primary key,
        name varchar(20),
        class_id int,
        foreign key (class_id) references classes(id)
    );
    ```

    ```bash
    mysql> desc classes;
    +-------+-------------+------+-----+---------+-------+
    | Field | Type        | Null | Key | Default | Extra |
    +-------+-------------+------+-----+---------+-------+
    | id    | int         | NO   | PRI | NULL    |       |
    | name  | varchar(20) | YES  |     | NULL    |       |
    +-------+-------------+------+-----+---------+-------+
    2 rows in set (0.00 sec)

    mysql> desc students;
    +----------+-------------+------+-----+---------+-------+
    | Field    | Type        | Null | Key | Default | Extra |
    +----------+-------------+------+-----+---------+-------+
    | id       | int         | NO   | PRI | NULL    |       |
    | name     | varchar(20) | YES  |     | NULL    |       |
    | class_id | int         | YES  | MUL | NULL    |       |
    +----------+-------------+------+-----+---------+-------+
    3 rows in set (0.00 sec)
    ```

    ```sql
    insert into classes values (1,'一班');
    insert into classes values (2,'二班');
    insert into classes values (3,'三班');
    insert into classes values (4,'四班');

    insert into students values (1001,'张三',1);
    insert into students values (1001,'张三',5); # ERROR
    delete from classes where id=4;
    ```

    1. 主表没有的数据，副表不能使用
    2. 主表中的记录被副表引用，是不可以被删除的