### SQL Server数据类型

![Image of Yaktocat](http://oyojovx0n.bkt.clouddn.com/01.png?e=1509444582&token=rah5Tr-k0fkmUfjSk-1k0KQPzitTP9co06CuG9P3:MnOejHzBqk8JJilQ2CUZdACRzdI)

![Image of Yaktocat](http://oyojovx0n.bkt.clouddn.com/02.png?e=1509447007&token=rah5Tr-k0fkmUfjSk-1k0KQPzitTP9co06CuG9P3:vA7QglcknOgBYekU8C6gVlzkSF4)

![Image of Yaktocat](http://oyojovx0n.bkt.clouddn.com/03.png?e=1509447177&token=rah5Tr-k0fkmUfjSk-1k0KQPzitTP9co06CuG9P3:iloRHjUK8i3CdlfYzQ1HxfPizZs)

![Image of Yaktocat](http://oyojovx0n.bkt.clouddn.com/04.png?e=1509447306&token=rah5Tr-k0fkmUfjSk-1k0KQPzitTP9co06CuG9P3:-sF3BSaw1zdJHl4LYGNqmwaIsDE)

![Image of Yaktocat](http://oyojovx0n.bkt.clouddn.com/05.png?e=1509447480&token=rah5Tr-k0fkmUfjSk-1k0KQPzitTP9co06CuG9P3:QpwJ5RDqk8XqZUlph7UFqijQqlM)

![Image of Yaktocat](http://oyojovx0n.bkt.clouddn.com/06.png?e=1509447540&token=rah5Tr-k0fkmUfjSk-1k0KQPzitTP9co06CuG9P3:GfrHomb7XtvsxzA7eNJ6mBy2Y48)

1. 获取所有表名 SELECT Name FROM DatabaseName..SysObjects Where XType='U' ORDER BY Name 

2. 获取表中所有字段名 SELECT Name FROM SysColumns WHERE id=Object_Id('TableName') 

### SQL Server 基本操作

### 创建数据库
```
CREATE DATABASE TestData
GO
```
### 创建表
以下代码是创建一个名为 ```Products```的简单表。该表中各列的名称为 ```ProductID```、```ProductName```、```Price```和
```ProductDescription```。```ProductID```列是表的主键。```int``varchar(25)```、```money```和```text```都是数据类型。
当插入或更改行时，只有```Price```和```ProductionDescription```列可以不包含数据。
```
CREATE TABLE dbo.Products  
   (ProductID int PRIMARY KEY NOT NULL,  
    ProductName varchar(25) NOT NULL,  
    Price money NULL,  
    ProductDescription text NULL)  
GO  
```
### 数据插入存在如下几种情况
基本语法如下: INSERT、表名、列的列表、VALUES，然后是要插入的值的列表。 
1. 第一种按照表的列表顺序插入数据 如下:
```
INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
    VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
GO  
```
2. 第二种是通过在字段列表(在圆括号中)中和值列表中均切换 ```ProductID```和```ProductName```的位置，更改提供参数的顺序
```
INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
    VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
GO  
```
3. 以下语句演示，只要值是按正确顺序列出的，列的名称就是可选的(可以不写)。此语法很常见，但是建议不要使用它，因为其他人了解代码会更困难。```NULL```
为```Price```列指定。
```
INSERT dbo.Products  
    VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
GO  
```
4. 只要在默认架构中访问和更改表，架构名称就是可选的。由于```ProductDescription```列允许 NULL 值，而且没有提供值，因此可以从语句中完全删除
```ProductDescription```列的名称和值。
```
-- Dropping the optional dbo and dropping the ProductDescription column  
INSERT Products (ProductID, ProductName, Price)  
    VALUES (3000, '3mm Bracket', .52)  
GO  
```
### 更新products 表
1. 键入并执行以下 ```UPDATE``` 语句，将第二种产品的 ```ProductName``` 从 ```Screwdriver```更改为```Flat Head Screwdriver```
```
UPDATE dbo.Produces
    SET ProductName = 'Flat Head Screwdriver'
    WHERE ProductID = 50
GO    
```
### 读取表中的数据
1. 键入并执行以下语句以读取 ```Products```表中的数据。
```
-- The basic syntax for reading data from a single table  
SELECT ProductID, ProductName, Price, ProductDescription  
    FROM dbo.Products  
GO  
```
2. 可以使用星号选择表中所有列。
```
SELECT * FROM Products
GO
```
3. 可以省略不希望返回的列。列将按列出它们的顺序返回。
```
-- Returns only two of the columns from the table  
SELECT ProductName, Price  
    FROM dbo.Products  
GO  
```
4. 使用```WHERE```子句可以限制返回给用户的行。
```
-- Returns only two of the records in the table  
SELECT ProductID, ProductName, Price, ProductDescription  
    FROM dbo.Products  
    WHERE ProductID < 60  
GO  
```
5. 可以在返回列中的值时使用它们，以下示例对 ```Price```列执行数学运算。除非通过使用```AS```关键字提供一个名称，
否则以此方式更改的列将没有名称。
```
-- Returns ProductName and the Price including a 7% tax  
-- Provides the name CustomerPays for the calculated column  
SELECT ProductName, Price * 1.07 AS CustomerPays  
    FROM dbo.Products  
GO  
```
### 删除权限和对象
1. 在删除对象之前，请确保使用正确的数据库:
```
USE TestData;
GO
```
2. 使用```DELETE```语句删除```Products```表中的所有行:
```
DELETE FROM Products;  
GO  
```
3. 使用```DROP```语句删除```Products```表:
```
DROP Table Products;  
GO  
```

### 使用 mssql 模块连接sql server数据库 代码如下:
```
var sql = require('mssql');
//连接方式1: 'mssql://用户名:密码@ip地址(无需端口号)/SqlServer名/数据库名称'
//连接方式2: 'mssql://用户名:密码@ip地址/数据库名称'
sql.connect('mssql://SA/:123@localhost').then(function(){
   // Query
   new sql.Request().query('select * from sys_user').then(function(recordset){
         console.log(recordset);
   }).catch(function(err){
       console.log(err);
   });  
   // Stored Procedure
}).catch(function(err){
   console.log(err);
})
```

### SqlServer查询表中各列名称、表中列数

查询表名为 tb_menu 的所有列名
```
select name from syscolumns where id=object_id('tb_menu')
```
查询表名为tb_menu的所有列名个数
```
select count(name) from syscolumns where id=object_id('tb_menu')
```
或者
```
select count(syscolumns.name)
from syscolumns , sysobjects
where syscolumns.id=sysobjects.id  and sysobjects.name = 'tb_menu'
```
### sql server 复制表结构

说明: 复制表(只复制结构,源表名:a 新表明: b)
```
SQL: select * into b from a where 1<>1
```

### 添加,删除,修改字段

通用式:
```
alter table [表名] add [字段名] 字段属性 default 缺省值 default 是可选参数
```
增加字段:
```
alter table [表名] add 字段名 smallint default 0 增加数字字段，整型，缺省值为0   
alter table [表名] add 字段名 intdefault 0 增加数字字段，长整型，缺省值为0  
alter table [表名] add 字段名 singledefault 0 增加数字字段，单精度型，缺省值为0   
alter table [表名] add 字段名 doubledefault 0 增加数字字段，双精度型，缺省值为0  
alter table [表名] add 字段名Tinyint default 0 增加数字字段，字节型，缺省值为0  
  
alter table[表名] add 字段名 text [null] 增加备注型字段,[null]可选参数  
alter table [表名] add 字段名 memo[null] 增加备注型字段,[null]可选参数  
  
alter table[表名] add 字段名 varchar(N) [null] 增加变长文本型字段大小 为N(1～255)  
alter table [表名] add 字段名 char[null] 增加定长文本型字段 大小固定为255  
  
alter table[表名] add 字段名 Datetime default 函数 增加日期型字段，其中函数 可以是 now(),date()等，表示缺省值  
(上面都是最常用的，还有其他的属性，可以参考下面的数据类型描述)  
```
删除字段:
```
alter table [表名] drop column 字段名
```
修改字段:
```
alter table [表名] alter column [字段名] nvarchar (50) null
```
修改变长文本型字段的大小:
```
alter table [表名] alter 字段名 varchar(N)
```
### 查询当前表的数据条数
```
select count(*) from tableName
```
### sql server 两张表筛选相同数据和不同数据
相同数据
```
select [字段名] from [表名] intersect select [字段名] from [表名]
```
不同数据
```
select [字段名] from [表名] except select [字段名] from [表名]
```
