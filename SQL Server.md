### 安装 SQL Server，并在 Ubuntu 上创建数据库  步骤如下:

1. 导入公共存储库 GPG 密钥:
```
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
```
2. 注册 Microsoft SQL Server Ubuntu 存储库:
```
sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)"
```
3. 运行以下命令，安装 SQL Server:
```
sudo apt-get update
sudo apt-get install -y mssql-server
```
4. 运行包安装完成后 mssql conf 安装并按照提示操作以设置 SA 密码，并选择你的版本。
```
sudo /opt/mssql/bin/mssql-conf setup
```
5. 配置完成后，请验证服务是否正在运行:
```
systemctl status mssql-server
```

### 安装 SQL Server 命令行工具
若要创建数据库，需要使用一种工具，可以在 SQL Server 上运行 Transact-SQL 语句进行连接。
以下步骤安装 SQL Server 命令行工具: sqlcmd 和 bcp。

1. 导入公共存储库 GPG 密钥:
```
curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
```
2. 注册 Microsoft Ubuntu 存储库:
```
sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list)"
```
3. 更新源列表，然后运行 unixODBC 开发人员包的安装命令:
```
sudo apt-get update
sudo apt-get install -y mssql-tools unixodbc-dev
```
4. 为方便起见，添加 ```/opt/mssql-tools/bin/```到你**路径**环境变量。这使您可以运行工具，而无需指定完整
路径。运行以下命令以修改**路径**登录会话和交互式/非-登录会话:
```
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
```
### 本地连接
#### 以下步骤使用 sqlcmd 本地连接到新的 SQL Server 实例。

1. 使用 SQL Server 名称 (-S),用户名 (-U)和密码 (-P)的参数运行 sqlcmd。因为用户进行本地连接，因此服务器名称为 ```localhost```。
用户名为 ```SA```,密码是在安装过程中为 SA 账户提供的密码。
```
sqlcmd -S localhost -U SA -P '<YourPassword>'
```
可以在命令行上省略密码，以收到密码输入提示。

如果以后决定进行远程连接，请指定 -S 参数的计算机名称或 IP 地址，并确保防火墙上的端口 1433 已打开。

2. 如果成功，会显示 sqlcmd 命令提示符: ```1>```。
3. 如果连接失败，请首先尝试根据错误消息诊断信息。然后查看 [连接故障排除建议](https://docs.microsoft.com/zh-cn/sql/linux/sql-server-linux-troubleshooting-guide#connection)。

### 新建数据库
以下步骤创建一个名为 ```TestDB```的新数据库。
1. 在 sqlcmd 命令提示符中，粘贴以下 Transact-SQL 命令以创建测试数据库:
```
CREATE DATABASE TestDB
```
2. 在下一行中，编写一个查询以返回服务器上所有数据库的名称:
```
SELECT Name from sys.Databases
```
3. 前两个命令没有立即执行。必须在新行中键入```GO```才能执行以前的命令:
```
GO
```
### 插入数据
接下来创建一个新表```Inventory```，然后插入两个新行。
1. 在 sqlcmd 命令提示符中，将上下文切换到新的```TestDB```数据库:
```
USE TestDB
```
2. 创建名为 ```Inventory```的新表:
```
CREATE TABLE Inventory (id INT, name NVARCHAR(50), quantity INT)
```
3. 将数据插入新表:
```
INSERT INTO Inventory VALUES (1, 'banana', 150); INSERT INTO Inventory VALUES (2, 'orange', 154);
```
4. 要执行上述命令的类型```GO```:
```
GO
```
### 选择数据
现在，运行查询以从 ```Inventory```表返回数据。
1. 通过 sqlcmd 命令提示符输入查询，以返回```Inventory```表中数量大于152的行:
```
SELECT * FROM Inventory WHERE quantity > 152;
```
2. 执行命令:
```
GO
```
### 退出 sqlcmd 命令提示符
要结束 sqlcmd 会话，请键入 ```QUIT```:
```
QUIT
```


