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
/*
    offset:
    offsetHeight: 获得元素高度 = height + border + padding
    offsetWidth: 获得元素宽度 = width + border + padding
    offsetLeft: 获得元素左外边框距离包含该元素的左内边框的距离(经过定位)
    offsetTop: 获得元素上外边框距离包含该元素的上内边框的距离(经过定位)
    offsetParent: 获得包含该元素的元素(定位)
    
    scroll用法:
    scroll是滚动条用法，即通过拖动条改变页面的位置，scroll相关属性:
    scrollHeight: 在没有滚动条的情况下，元素内容的总高度
    scrollWidth: 在没有滚动条的情况下，元素内容的总宽度
    scrollLeft: 被隐藏在内容区域左侧的像素数。通过设置这个属性可以改变元素的滚动位置
    scrollTop: 被隐藏在内容区域上方的像素数。通过设置这个属性可以改变元素的滚动位置
    
    浏览器兼容性问题
    
    混杂模式下，既没有声明DTD时
    混杂模式: document.compatMode === "BackCompat"
    html元素的纵向滚动值 scrollTop 的值为 document.body.scrollTop;
    
    标准模式下
    标准模式: document.compatMode === "CSS1Compat"
    html元素的纵向滚动值 scrollTop 的值为 document.documentElement.scrollTop;
    
    高版本浏览器中(ie9以上)都支持
    html元素的纵向滚动值 scrollTop 的值可以用 window.pageYOffset;
    兼容写法: scrollTop = window.pageYOffset || document.body.scrollTop || document.documentElement.scrollTop;
*/
window.onscroll = ()=>{
    let scrollTop = window.pageYOffset || document.body.scrollTop || document.documentElement.scrollTop;
    console.log(scrollTop); 
}
```
5. 项目写的时候要整理好整体逻辑，一定要整理清楚整个架构，尤其是大的素材要考虑是否切割后在去做，不然加载的时候会慢，
图片都要进行压缩处理，引入的文件要整理好。所有的素材也整理完毕，尽可能使用html5语义化新标签，js代码也要整理清楚。
