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
4. 使用递归方式存取数据(防止数据丢失)。
```
var i = -1;
loop();
function loop(){
   i++;
   if(xxx[i]){
   console.log('i == ', i);
   
   // data 部分
   
    var dat = 'INSERT INTO TABLENAME VALUES(data)';
    new sql.Request().query(dat).then(function(){
      loop();
    })
   }
}
```
5. 接口部分。
```
var md5 = crypto.createHash('md5');
var password = md5.update('#$&'+xxx_ID+'&&#').digest('hex'); // xxx_ID(两边需要一致)是纯number或者是数值的string
var key = CryptoJS.HmacSHA1(password, 'xxx');
var base = new Base64(); // Base64()是加密函数
var result3 = base.encode(key.toString());

var options = {
  method: 'PUT', //根据对应API决定method方法(POST, GET)
  url: 'https://xxx.xxx.xxx' //接口部分 API 
  headers:{
    //headers 中为接口部分对应部分，可以通过postman获取，或者对面接口人员提供。
    'postman-token': 'xxx',
    'cache-control': 'no-cache',
    'content-type': 'application/json'
  },
  body:{
    //body中则是向对面发送的内容
    name: 'Lisi',
    age: 18,
    hobby: 'study',
    token: result3
  },
  json: true
};

request(options, function(error, response, body) {
   if(!error){
      console.log(body); // body 为接口调用成功后返回的内容
   } else {
      console.error(error); // error 为接口调用失败后返回的内容
   }
});
```
### 整体逻辑
读取del文件获得data，然后对data进行处理，本地数据库创建两张表格，数据存储分为首次导入和后续导入，

