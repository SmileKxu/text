### 项目整理点:

1. 监听手机横竖屏:使用媒体查询配合js来管理，代码如下:
```html
@media screen and (orientation: portrait){
    .test::after{
      content: '竖屏';
    }
}

@media screen and (orientation: landscape){
    .test::after{
      content: '横屏';
    }
}
```
```js
<script>
  //通过访问对象的matches属性:
  let mql = window.matchMedia('(orientation: portrait)');
  
  const handleOrientationChange = (mql) => {
    if(mql.matches){
      console.log('portrait'); //打印竖屏
    } else {
      console.log('landscape'); //打印横屏
    }
  }
  
  //打印日志
  handleOrientationChange(mql);
  
  //监听屏幕模式的变化
  
  mql.addListener(handleOrientationChange);

<script/>
```
2. 百度统计来进行网站数据统计，[百度统计官网](https://tongji.baidu.com/),js代码如下:
```js
<script>
// 这段代码在百度统计输入要统计的网站就会生成，然后引入就可以
var _hmt = _hmt || [];  
(function() {
    var hm = document.createElement("script");
    hm.src = "https://hm.baidu.com/hm.js?4b3dc673329f3d9fffdb86156998b774";
    var s = document.getElementsByTagName("script")[0];
    s.parentNode.insertBefore(hm, s);
})();
</script>
```
3. 对于Android移动端的图片会被手机点击查看的取消方法，取消图片的默认行为:
```js
$('img').click(function(event){
  event.preventDefault();
})
```
4. 鼠标滑轮事件:在电脑监听鼠标滑轮事件以及手机监听鼠标滑轮事件的方法，代码如下:
```js
  
```
