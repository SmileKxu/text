### 微信公众号(测试号)开发流程个人总结:

微信公众号开发需要认证，而个人申请的微信公众号不可以认证，对于功能的需求那么就可以申请微信公众测试号。

申请网站入下: [https://mp.weixin.qq.com/debug/cgi-bin/sandboxinfo?action=showinfo&t=sandbox/index](https://mp.weixin.qq.com/debug/cgi-bin/sandboxinfo?action=showinfo&t=sandbox/index)

然后使用手机微信扫一扫登录，进入公众平台界面。该界面开始会给测试账号信息，分别为 appID 与 appsecret，这两个信息可以获取 access_token 的值。

然后需要首要添加的内容为接口配置信息，有两个需要输入值的地方 URL 和 Token。这里可以阅读 [消息接口使用指南](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421135319)

这里的 URL 是开发者用来接收微信消息和事件的接口 URL。Token 可以由开发者任意填写，用作生成签名(接口使用指南原话)。

这里的操作就是这样，我这里是有服务器的，而且我是基于 node.js 微信号测试(接口配置信息)验证服务器的 URL，我只需要在服务器建立一个js文件然后绑定端口，
输入 Token，然后使用 node 启动就可以。代码如下:
```
var PORT=8080;                 //监听8080端口号
var http=require('http');  
var qs=require('qs');
var TOKEN='gvshidai';           //必须与测试号所填写的Token相同

function checkSignature(params,token){
    var key=[token,params.timestamp,params.nonce].sort().join(''); 
     //将token （自己设置的） 、timestamp（时间戳）、nonce（随机数）三个参数进行字典排序
    var sha1=require('crypto').createHash('sha1');
     //将上面三个字符串拼接成一个字符串再进行sha1加密
    sha1.update(key);
    return sha1.digest('hex') ==params.signature;
     //将加密后的字符串与signature进行对比，若成功，返回echostr
}

var server=http.createServer(function (request,response) {
   var query=require('url').parse(request.url).query;
    var params=qs.parse(query);

    console.log(params);
    console.log("token :",TOKEN);


    if(!checkSignature(params,TOKEN)){
        //如果签名不对，结束请求并返回
        response.end('signature fail');
    }

    if (request.method == "GET") {
        //如果请求是GET，返回echostr用于通过服务器有效校验
        response.end(params.echostr);
    }else{
        //否则是微信给开发者服务器的POST请求
        var postdata='';
        request.addListener("data",function(postchunk){
            postdata+=postchunk;
        });
        //获取到了POST数据
        request.addListener("end",function(){
            console.log(postdata);
            response.end('success ');
        });
    }
});

server.listen(PORT, function () {
    console.log('Server running at port:'+PORT);
});
```
使用 node 启动该js文件就可以在测试号接口配置信息配置了，URL 为 ```http://xxx.xx.xxx:8080```, Token 则就是js文件内输入的Token，那么接口配置信息
就搞定了。

接下来是输入JS接口安全域名，这个安全域名就是填写自己网站的域名，输入一个相关的域名。

然后使用微信扫描二维码关注测试公众号，就可以在手机上关注当前测试的微信公众号。

在页面的最后面提供了体验接口权限表，可以很详细的查看都可以调用那些接口。

然后我测试了自定义菜单功能，[自定义菜单创建接口](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421141013)

细节部分仔细查看官方文档即可，包括自定义菜单的类别，以及不同按钮等等。这里直接拉到页面的最下方有一个[使用网页调试工具调试该接口](https://mp.weixin.qq.com/debug/cgi-bin/apiinfo?t=index&type=%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8F%9C%E5%8D%95&form=%E8%87%AA%E5%AE%9A%E4%B9%89%E8%8F%9C%E5%8D%95%E5%88%9B%E5%BB%BA%E6%8E%A5%E5%8F%A3%20/menu/create)

打开该页面可以看到是微信公众平台接口调试工具，按照使用说明填写字段，这里获得的 access_token 就是上面通过 appID 与 appsecret 获得。

获得 access_token 在文档中打开 [接口在线调试](https://mp.weixin.qq.com/wiki?t=resource/res_main&id=mp1421137524),在这个页面的最下边
可以看到 [进入微信公众平台接口调试工具](https://mp.weixin.qq.com/debug/),进入该页面就可以获得 access_token。

输入 appid 与 secret 正确后会出现绿色的字体校验通过，这时点击检查问题就可以获得，access_token 的值就是橘色的部分，最下面的提示部分成功后会提示
Request successful。

然后在 body 中按照文档格式输入内容即可，这是打开微信查看就会发现自己添加的自定义菜单。






