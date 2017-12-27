### 使用 MediaDevices.getUserMedia() 方法调取摄像头功能

MediaDevices.getUserMedia() 方法提示用户允许使用一个视频和/或一个音频输入设备，例如相机或屏幕共享和/或麦克风。
如果用户给予许可，就返回一个Promise对象，MediaStream对象作为此Promise对象的Resolved[成功]状态的回调函数参数。
相应的，如果用户拒绝了许可，或者没有媒体可用的状况下，PermissionDeniedError或者NotFoundError作为此Promise的Rejected[失败]
状态的回调函数参数。

### 语法
```
navigator.mediaDevices.getUserMedia(constraints)
.then(function(mediaStream){ ... })
.catch(function(error) { ... } )
```

### 参数
constraints 作为一个MediaStreamConstraints对象，指定了请求的媒体类型和相应的参数。
constraints 参数是一个包含了 video 和 audio 两个成员的 MediaStreamConstraints 对象，用于说明请求的媒体类型。
必须至少一个类型或者两个同时可以被指定。如果浏览器无法找到指定的媒体类型或者无法满足相对应的参数要求，那么返回的Promise
对象就会处于rejected[失败]状态，NotFoundError作为rejected[失败]回调的参数。

以下同时请求不带任何参数的音频和视频:
```
{ audio: true, video: true }
```
当由于隐私保护的原因，无法访问用户的摄像头和麦克风信息时，应用可以使用额外的constraints参数请求它所需要或者想要的摄像头和
麦克风能力。下面演示了应用想要使用 1280 * 720 的摄像头分辨率:
```
audio: true,
video: { width: 1280, height: 720 }
```
浏览器会试着满足这个请求参数，但是如果无法准确满足此请求中参数要求或者用户选择覆盖了请求中的参数时，有可能返回其它的分辨率。

强制要求获取特定的尺寸时，可以使用关键字min,max,或者exact(就是 min == max).以下参数表示要求获取最低为 1280 * 720的分辨率。
```
{
audio: true,
video: {
   width: { min: 1280 },
   height: { min: 720 }
  }
}
```
如果摄像头不支持请求的或者更高的分辨率，返回的Promise会处于rejected状态，NotFoundError作为rejected回调的参数，
而且用户将不会得到要求授权的提示。

造成不同表现的原因是，相对于简单的请求值和ideal关键字而言，关键字 min, max, 和 exact 有着内在关联的强制性，请看一个更详细的例子:
```
{
audio: true,
video: {
    width: { min: 1024, ideal: 1280, max: 1920 },
    height: { min: 776， ideal: 720, max: 1080 }
  }
}
```
当请求包含一个ideal(应用最理想的)值时，这个值有着更高的权重，意味着浏览器会先尝试找到最接近指定的理想值的
设定或者摄像头(如果设备拥有不止一个摄像头)。

并不是所有的 constraints 都是数字。例如，在移动设备上面，如下的例子表示优先使用前置摄像头(如果有的话):
```
{ 
  audio: true,
  video: {
    video: { facingMode: 'user' }
  }
}
```
强制使用后置摄像头，请用:
```
{
  audio: true,
  video: {
    facingMode: { exact: 'environment' }
  }
}
```

### 返回值
返回一个 Promise，这个Promise成功后的回调函数带一个 MediaStream 对象作为其参数。

### 异常
返回一个失败状态的Promise，这个Promise失败后的回调函数带一个DOMException对象作为其参数。
可能的异常有:
#### AboutError [中止错误]
尽管用户和操作系统都授予了访问设备硬件的权利，而且未出现可能抛出NotReadableError异常的硬件问题，
但仍然有一些问题出现导致了设备无法被使用。
#### NotAllowedError [拒绝错误]
用户拒绝了当前的浏览器实例的访问请求；或者用户拒绝了当前会话的访问；或者用户在全局范围内拒绝了所有媒体访问请求。
#### NotFoundError [找不到错误]
找不到满足请求参数的媒体类型
#### NotReadableError [无法读取错误]
尽管用户已经授权使用相应的设备，操作系统上某个硬件、浏览器或者网页层面发生的错误导致设备无法被访问。
#### TypeError [类型错误]
constraints对象未设置[空]，或者都被设置为false。

### 示例
#### 使用Promise
这个例子把返回的MediaStream对象赋值给合适的元素。
``` 
var p = navigator.mediaDevices.getUserMedia({ audio: true, video: true });

p.then(function(mediaStream){
   var video = document.querySelector('video'); //调取摄像头需要用到video标签，获取的资源会在video上显示
   video.src = window.URL.createObjectURL(mediaStream);
   video.onloadedmetadata = function(e){
      // Do something with the video here.
   }
})

p.catch(function(err){
  console.log(err.name);
}); // always check for errors at the end.
```
### 前置或者后置摄像头
在移动设备(电话)上
```
var front = false;
document.getElementById('filp-button').onclick = function(){
    front = !front;
};

var constraints = { video: { facingMode: (front ? "user" : "environment" ) } };
```
以上所有内容都是参考[Mozilla](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia)
