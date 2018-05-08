### MySql 数据库学习

#### win10 安装MySql过程如下:

1. 从官方网站下载MySql安装到指定目录。[MySql官网](https://dev.mysql.com/downloads/file/?id=476233)

2. 然后在管理员模式下进入cmd，进入我们安装的目录下，输入安装目录 mysqld -install。

3. 配置MySql，在管理员模式下在 install后继续输入命令 mysqld --initialize，回车执行命令后需要等待一小会，
这个过程会在MYSQL的解压目录下生成一个data文件夹，里面会有一个后缀名为.err结尾的文件，这个文件中包含着初次
使用MYSQL时生成的一个临时用随机密码，我们要找到这个随机密码才能登录使用。

4. 需要配置一下MYSQL的启动文件，在解压目录下新建一个.ini格式文件my.ini，然后以记事本格式打开写入下面代码:
```
[mysqld]
basedir=D:\mySQL\mysql-8.0.11-winx64\mysql-8.0.11-winx64
datadir=D:\mySQL\mysql-8.0.11-winx64\mysql-8.0.11-winx64\data
port=3306
```
这上面basedir、datadir后面是解压MYSQL的路径，写完后保存就OK。

5. 启动MYSQL服务，输入如下命令
```
net start mysql
```
输入如下命令登录MYSQL:
```
mysql -u root -p
```
这时需要输入从.err文件中获取到的那个密码然后就进入了mysql。
为了方便登录使用MYSQL，我们可以自己设定下每次登录MYSQL时输入密码，输入以下命令设置登录密码:
```
set password for root@localhost=password('xxxxxxxx');
```
6. 将MYSQL配置到环境变量里，这个就是正常的环境变量配置方法，最后到bin\目录下。

#### 数据库基本概念
数据库文件: 在计算机中具体的来说，一个关系型数据库可以看作一个数据库文件，我们通过对数据库文件的操作达到操作数据
库中数据的目的。在使用数据库前我们都需要创建这个"数据库文件"。关系型数据库文件一般以".db"作为后缀。

表: 你可以将数据库存储想象为一个表格，关系型数据库都是通过表来整理数据的。一个数据库中可以包含多个表。每个表在数
据库中都有自己唯一的名字。

字段: 就像我们日常做的表格一样，表中的每一列代表着一项，每一项都有自己的名称。我们跟表中的这些项(列)称之为字段。

记录: 表中的每一行都是一条记录。

操作: 增删改查系列0.0    在mysql交互模式下语句操作都是以"；"作为结束标志。

mysql常用命令: help(查看命令帮助) quit或exit(退出mysql操作) show databases: 显示数据库文件列表
use <database>(打开数据库) show tables(显示数据库所有表名) desc <table_name>:查看表的结构

#### 语句主要可以划分为以下三类:
* DDL语句(数据定义)
这些语句定义了不同的数据段、数据库、表、列、索引等数据库对象。常用的关键字包括create、drop、alter等
* DML语句(数据操纵)
用于添加、删除、更新和查询数据记录，并检查数据完整性。常用关键字包括insert、delete、update、和select的等。
* DCL语句(数据控制)
用于控制不同数据段直接的许可和访问级别的语句。这些语句定义了数据库、表、字段、用户和访问权限和安全级别。
主要的语句关键字有grant、revoke等。
