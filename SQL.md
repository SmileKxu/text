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

