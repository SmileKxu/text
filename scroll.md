- 页可见区域宽： document.body.clientWidth;
- 网页可见区域高： document.body.clientHeight;
- 网页可见区域宽： document.body.offsetWidth (包括边线的宽);
- 网页可见区域高： document.body.offsetHeight (包括边线的宽);
- 网页正文全文宽： document.body.scrollWidth;
- 网页正文全文高： document.body.scrollHeight;
- 网页被卷去的高： document.body.scrollTop;
- 网页被卷去的左： document.body.scrollLeft;
- 网页正文部分上： window.screenTop;
- 网页正文部分左： window.screenLeft;
- 屏幕分辨率的高： window.screen.height;
- 屏幕分辨率的宽： window.screen.width;
- 屏幕可用工作区高度： window.screen.availHeight

实现懒加载效果，需要引入 Lazy load，这是依赖于 jQuery 的js文件，首先引入:
```
<script type="text/javascript" src="jquery.js"></script>
<script type="text/javascript" src="jquery.lazyload.js"></script>
```
对于懒加载的图片，图片的路径不再是 src ，图像的地址必须放在 data-original 属性上，给懒加载
图像一个特定 class 方便对图像插件捆绑。代码如下:
```
<img class='lazy' data-original='./images/example.jpg'/>
```
JavaScript代码如下:
```
$(function(){
  $('.lzay').lazyload(); 
})
```
这将使所有 class 为 lazy 的图片将被延迟加载(图片必须设置width 和 height，否则插件可能无法正常工作)。
### 设置临界点
默认情况下图片会在出现屏幕时加载，如果想提前加载图片，可以设置 threshold 选项，设置 threshold 为 200 令
图片在距离屏幕 200 像素时提前加载。JavaScript代码:
```
  $('img .lazy').lazyload({
      threshold : 200
  });
```
### 设置事件来触发加载
可以使用jQuery事件(click, mouseover)，也可以使用自定义事件，当图片出现在屏幕上时，触发事件才加载图片。JavaScript代码:
```
  $('img .lazy').lazyload({
    event: 'click',  //当图片显示时，点击图片才加载图片
  });
```
### 使用特效:
默认情况图片显示加载调用 show()。可以使用自己想要的效果(fadeIn、slideDown等)。JavaScript代码:
```
   $('img .lazy').lazyload({
      effect: 'fadeIn'
   });
```
