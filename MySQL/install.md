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
