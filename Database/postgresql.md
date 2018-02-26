## 下载安装
* windows版本
    <https://www.postgresql.org/download/>

* Ubuntu版本
    安装文档（选择适合的版本，14.04为例）
    <https://www.postgresql.org/download/linux/ubuntu/>
    
1.创建文件
```
/etc/apt/sources.list.d/pgdg.list
```
2.在文件中添加以下行
```
deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main
```  
3.依次执行
```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | \
sudo apt-key add -
sudo apt-get update
apt-get install postgresql-9.6
```
 
## 配置
   [参考](https://www.cnblogs.com/z-sm/archive/2016/07/05/5644165.html)
    
### 修改数据库默认管理员账号的密码
    sudo -u postgres psql
    postgres=# alter user postgres with password '123456';
    
    删除管理员密码命令：sudo -u postgres psql -d postgres
    
### 配置数据库以允许远程连接访问

* 修改监听地址
```
sudo vim /etc/postgresql/9.6/main/postgresql.conf 
将 #listen_addresses = 'localhost' 的注释去掉并改为 listen_addresses = '*' 
```
* 修改可访问用户的IP段
```
sudo gedit /etc/postgresql/9.6/main/pg_hba.conf 
在文件末尾添加：host    all    all      192.168.31.0/24         md5
```
其中：192.168.31.0/24 表示 192.168.31.0~ 192.168.31.255的地址均可访问，24表示非固定（32表示固定地址）
   
* 重启数据库
```
sudo /etc/init.d/postgresql restart
```

### 添加新用户和新数据库

运行系统用户"postgres"的psql命令，进入客户端：
`sudo -u postgres psql`

创建用户"tom"并设置密码：
`postgres=# create user tom with password '123456';`

创建数据库practicedb，所有者tom：
`postgres=# create database practicedb owner tom;`

也可以使用权限操作将数据库的所有权限赋予用户
`grant all privileges on database practicedb to tom;`

---
## PostgreSQL基本操作

通过 `sudo -u postgres psql` 进入，提示符变成： `postgres=#  `
```
\password：设置密码
\q：退出
\h：查看SQL命令的解释，比如\h select。
\?：查看psql命令列表。
\l：列出所有数据库。
\c [database_name]：连接其他数据库。
\d：列出当前数据库的所有表格。
\d [table_name]：列出某一张表格的结构。
\du：列出所有用户。
\e：打开文本编辑器。
\conninfo：列出当前数据库和连接的信息。
```
### 几个常用的操作
```
 \du 查看数据库账户
 \c [dbname]: 切换其它数据库
 \d 列出当前数据库的所有表格
 \d [表名]：列出指定表结构
```
---
## 博客地址
http://blog.csdn.net/zhouli2008/article/details/79376846
