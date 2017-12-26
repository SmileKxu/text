### Second tasks summary

这个项目的功能是由客户那边买的，功能已经实现，但是需要按照功能文档进行调用。

主要分为以下几点:

1. 仔细阅读理解功能文档(因为是纯英文所以理解有点惨)，了解其功能模块。
2. 从功能文档中滤清思路，将功能实现的逻辑整理好知道如何下手。
3. 使用node.js与express实现，在node.js中使用https的配置等。

大致分为这三点，其实仔细阅读文档别着急就没那么难，根据文档调用方法引入两个js文件，
并且使用到了 iframe 标签(跨域)，然后就可以调用方法。

方法调用后逻辑方面主要根据其函数的返回值，函数onTryLiveNotify有两个参数，message和data，所有的判断都是根据这两个状态
来进行判断。
当初始化完成后:
```
message == "initializationFinished";
data == true;
```
此时就可以调用摄像头，然后若状态改变为 trackingStatusChanged 时，此时就会根据内容去下载资源，资源下载完毕后处于显示状态。
```
message == "trackingStatusChanged";
data == true;
```
当此时的data为false时，那么就会让资源隐藏，然后在其true后在显示。摄像功能逻辑部分大致处理就是这样。

node.js本身就是一个服务器，所以将整个文件放入到服务器上指定域名就可以访问，但是若要访问https，那么需要引入证书，代码如下:
```
在bin目录下的www文件中，引入https模块和fs模块:
var https = require('https');
var fs = require('fs');

然后将证书导入，我这里使用的是pfx，
const options = {
  pfx: fs.readFileSync('xxx/xxx/xxx.pfx'), //将pfx文件按照路径导入
  passphrase: '123456'  // passphrase 的值为证书的密码(是字符串格式)  
};
var sslport = normalizePort(process.env.PORT || '8000'); //定义https的端口号
var httpsServer = https.createServer(options, app); 
httpsServer.listen(sslport);
```
node.js 使用https部分可以查看官方文档。

对于PFX证书可以使用OpenSSL转换成PEM证书
```
X509转PFX:
openssl pkcs12 -export -inkey test.key -in test.cer -out test.pfx
PFX转X509：
openssl pkcs12 -in test.pfx -nodes -out test.pem 
openssl rsa -in test..pem -out test.key
openssl x509 -in test..pem -out test.crt 
```
对于node.js导入https启动若出现这个错误
![Err Image](https://sfault-image.b0.upaiyun.com/372/198/3721983082-59bf640cac8a4_articlex)

那么就是 pfx 文件与 passphrase 不匹配或 pfx 文件损坏导致的。



