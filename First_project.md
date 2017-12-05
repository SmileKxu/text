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
6. 加密部分 Base64()
```
 //生成token

 function Base64() {

     // private property
     _keyStr = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";

     // public method for encoding
     this.encode = function (input) {
         var output = "";
         var chr1, chr2, chr3, enc1, enc2, enc3, enc4;
         var i = 0;
         input = _utf8_encode(input);
         while (i < input.length) {
             chr1 = input.charCodeAt(i++);
             chr2 = input.charCodeAt(i++);
             chr3 = input.charCodeAt(i++);
             enc1 = chr1 >> 2;
             enc2 = ((chr1 & 3) << 4) | (chr2 >> 4);
             enc3 = ((chr2 & 15) << 2) | (chr3 >> 6);
             enc4 = chr3 & 63;
             if (isNaN(chr2)) {
                 enc3 = enc4 = 64;
             } else if (isNaN(chr3)) {
                 enc4 = 64;
             }
             output = output +
                 _keyStr.charAt(enc1) + _keyStr.charAt(enc2) +
                 _keyStr.charAt(enc3) + _keyStr.charAt(enc4);
         }
         return output;
     }

     // public method for decoding
     this.decode = function (input) {
         var output = "";
         var chr1, chr2, chr3;
         var enc1, enc2, enc3, enc4;
         var i = 0;
         input = input.replace(/[^A-Za-z0-9\+\/\=]/g, "");
         while (i < input.length) {
             enc1 = _keyStr.indexOf(input.charAt(i++));
             enc2 = _keyStr.indexOf(input.charAt(i++));
             enc3 = _keyStr.indexOf(input.charAt(i++));
             enc4 = _keyStr.indexOf(input.charAt(i++));
             chr1 = (enc1 << 2) | (enc2 >> 4);
             chr2 = ((enc2 & 15) << 4) | (enc3 >> 2);
             chr3 = ((enc3 & 3) << 6) | enc4;
             output = output + String.fromCharCode(chr1);
             if (enc3 != 64) {
                 output = output + String.fromCharCode(chr2);
             }
             if (enc4 != 64) {
                 output = output + String.fromCharCode(chr3);
             }
         }
         output = _utf8_decode(output);
         return output;
     }

     // private method for UTF-8 encoding
     _utf8_encode = function (string) {
         string = string.replace(/\r\n/g, "\n");
         var utftext = "";
         for (var n = 0; n < string.length; n++) {
             var c = string.charCodeAt(n);
             if (c < 128) {
                 utftext += String.fromCharCode(c);
             } else if ((c > 127) && (c < 2048)) {
                 utftext += String.fromCharCode((c >> 6) | 192);
                 utftext += String.fromCharCode((c & 63) | 128);
             } else {
                 utftext += String.fromCharCode((c >> 12) | 224);
                 utftext += String.fromCharCode(((c >> 6) & 63) | 128);
                 utftext += String.fromCharCode((c & 63) | 128);
             }

         }
         return utftext;
     }

     // private method for UTF-8 decoding
     _utf8_decode = function (utftext) {
         var string = "";
         var i = 0;
         var c = c1 = c2 = 0;
         while (i < utftext.length) {
             c = utftext.charCodeAt(i);
             if (c < 128) {
                 string += String.fromCharCode(c);
                 i++;
             } else if ((c > 191) && (c < 224)) {
                 c2 = utftext.charCodeAt(i + 1);
                 string += String.fromCharCode(((c & 31) << 6) | (c2 & 63));
                 i += 2;
             } else {
                 c2 = utftext.charCodeAt(i + 1);
                 c3 = utftext.charCodeAt(i + 2);
                 string += String.fromCharCode(((c & 15) << 12) | ((c2 & 63) << 6) | (c3 & 63));
                 i += 3;
             }
         }
         return string;
     }
 }
```
### 整体逻辑
读取del文件获得data，然后对data进行处理，本地数据库创建两张表格，数据存储分为首次导入和后续导入，首先数据先全部存入B表，存储完毕后，判断A表内是否存在内容，若不存在，则是首次导入的过程，此时使用递归的方式将B表所有内容存到A表，在A表存储数据库的返回值内，调用接口，将数据通过API发送过去，当数据添加完毕后，(在else中)然后两张表进行对比，若完全相同，关闭数据库sql.close()。若A表存在内容，则不适为首次导入，那么A、B两0张表进行对比(只比ID)，找到A不存在的ID部分，然后从B表中查找出来，添加到A表，在A表数据库添加内走接口部分。当数据添加结束后，(在else中)然后两张表整体比较，找到不同的部分，进行update。当所有的条件都已经不满足时，就是所有的操作都结束时，再其else中写下一个操作。
