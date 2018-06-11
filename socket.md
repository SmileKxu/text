## 通信 API

HTML5新增的通讯相关的两个功能:跨文档消息传输功能与使用Web Sockets API 来通过socket端口传递数据的功能。

使用跨文档消息传输功能，你可以再不同网页文档、不同端口、不同域之间进行消息的传递。

使用Wrb Sockets API，你可以让客户与服务器通过socket端口来传递数据，这样做的好处是可以实现数据推送技术
服务器端不再是被动的等待客户端发出的请求，只要客户端与服务器端建立了一次连接之后，服务器端就可以在需要的
时候，主动地将数据推送到客户端，直到客户端显示关闭这个连接。

### 跨文档消息传输的基本知识

HTML5 提供了在页面文档之间互相接收与发送信息的功能。使用这个功能，只要获取到网页所在窗口对象的实例，不仅
同源(域+端口号)的Web网页之间可以互相通信，甚至可以实现跨域通信。

首先，要想接受从其他窗口那里发过来的消息，就必须对窗口对象的message事件进行监视，代码如下所示:
```js
window.addEventListener('message', () => {...}, false);
```
使用window对象的postMessage方法向其他窗口发送消息，该方法定义如下:
```js
otherWindow.postMessage(message, targetOrigin);
```
该方法使用两个参数，第一个参数为所发送的消息文本，也可以是任何JavaScript对象(通过JSON转换对象为文本)；
第二个参数为接收消息的对象窗口的URL地址`http://localhost:3000/。`可以在URL地址字符串中使用通配符`"*"`
指定全部地址，建议使用准确的URL地址。otherWindow为要发送窗口对象的引用，可以通过window》open返回该对象，
或者通过对window.frames数组指定序号(index)或名字的方式来返回单个frame所属的窗口对象。

下面展示一个主页面与主页面中的iframe子页面之间的互相通信。首先，主页面向iframe子页面发送消息，iframe子页面
接受消息，显示在本页面中，然后像主页面返回消息。最后，主页面接受消息，然后将该消息打印。该demo是由node测试，两个
页面均为不同端口然后实现跨域通信。

首先是主页面的代码：
```html
<DOCTYPE!>
 <html>
 <head>
  <meta charset='UTF-8'>
  <tittle>跨域通信示例</tittle>
 <head>
 <body>
    <h1>跨域通信实例</h1>
    <iframe id='iframe' width='400' src='http://192.168.1.142:4000/index'></iframe>
 
 <script>
    let iframe = document.querySelector('#iframe');
    // 监听 message 事件
    window.addEventListener('message', (event) => {
      // 忽略指定url之外的页面传来的消息
      if(event.orign != 'http://192.168.1.142:4000' ){
          return;
      }
      // 打印传递过来的消息
      console.log('从' + event.origin + '那里传过来的消息：\n\'' + event.data + '\'');
    },false);
    
    const handler = () => {
        let win_iframe = window.frames[0];
        // 传递消息
        win_iframe.postMessage('Hello', 'http://192.168.1.142:4000');
    }
  
  iframe.onload = () => {
      handler();
  }
   
 </script>
 </body>
 </html>
```
下面是主页面内iframe的页面的代码:
```html
<DOCTYPE!>
<html>
  <head>
    <meta charset='utf-8'>
    <tittle></tittle>
  </head>
  <body>
    <h1>Hello World</h1>
    <h2></h2>
  
  <script>
    let h2 = document.querySelector('h2');
    window.addEventListener('message', (event) => {
      console.log('event.origin = ', event.origin);
      console.log('event.data = ', event.data);
      console.log('event.source = ', event.source);
 
      if(event.origin != 'http://192.168.1.142:3000'){
        return;
      }
 
      h2.innerHTML = '从' + event.origin + '那里传来的消息。<br>\'' + event.data + '\'';
 
      event.source.postMessage('您好，这里是' + this.location, event.origin);
      
    }, false);
  
  </script>
  </body>
</html>
```

下面对本示例中几个关键之处进行补充说明。
1. 通过对window对象的message事件进行监听，可以接收消息。
2. 通过访问message事件的origin属性，可以获取消息的发送源(发送源只包括域名和端口号，为了不接收其他源恶意
   发送过来的消息，最好对发送源做个检查)。
3. 通过访问message事件的data属性，可以获取消息内容(可以是任何JavaScript对象)。
4. 使用postMessage方法发送消息。
5. 通过访问message事件的source属性，可以获取消息发送源的窗口对象(准确地说，应该是窗口代理对象)。









