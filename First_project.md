### 工作内容:
1. 读取 del 文件内容，处理文件信息存储数据。
2. 使用递归的方式逐条存取数据，将数据存储到数据库中(sql server)。
3. 对表中信息比对，得到add、update、delete的数据，通过对应的 API 向对面发送信息，然后对数据库进行修改。

### 使用模块:
```
var fs = require('fs'); // fs模块
var sql = require('mssql'); // mssql node.js连接sql server使用模块
var request = require('request'); // 接口部分发送请求
var crypto = require('crypto');
var CryptoJS = require('crypto-js')  // 这两个 crypto模块是接口部分加密
var http = require('http');
var schedule = require('node-schedule'); // node.js定时任务模块
```
### 具体流程:
1. del文件名称会根据当天时间与前缀拼接。
```
var d = new Date();
var year = d.getFullYear();
var month = d.getMonth() + 1; // getMonth()获得的时间是 0~11，所以+1。
var day = d.getDate();

// 获得的时间都是 number 类型。

function handler(num){
  return num > 9 ？ num : '0' + num;
}

// handler 函数对于小于 9 的数会改成 string 类型 '0' + num。
var file_name = 'xxx_' + year + month + date + '.del'; 
```
2. 读取文件按行读取。
```
var s = readLine(fs.createReadStream('/文件路径/xxx.del'),{
       newline: '\n',
}); // 读取del文件，以'\n'为分隔符

s.on('data', function(data){
    var arr = data.split(':');
    s.next();
}); // 对读取的data进行处理

s.on('end', function(){
    在 'end' 中可以得到处理后的data，然后在这里进行后续的操作。
});
```
3. 连接数据库存储数据。
```
// 引用 mssql 模块后连接数据库如下:

sql.connect('mssql://sa:sql_password@localhost/DATABASE').then(function(){

}).catch(function(err){
   console.log('catcherr:' + err);
})
```
