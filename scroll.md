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
### 总体设置
```
   $('img .lazy').lazyload({
   
      placeholder: 'img/grey.gif',   //用图片提前占位
      // placeholder, 值为某一图片路径.此图片用来占据将要加载图片的位置，待图片加载时，占位图则会隐藏
      
      effect: 'fadeIn',    // 载入时使用何种效果
      // effect(特效),值有show(直接显示),fadeIn(淡入),slideDown(下拉)等，常用fadeIn
      
      threshold: 200,  // 提前200px开始加载
      // threshold,值为数字，代表页面高度.如设置为200，表示滚动条在离目标位置还有200的高度时就开始加载图片，可以做到不让用户察觉
      
      event: 'click', // 事件触发时才加载
      // event,值有click(点击),mouseover(鼠标划过),sporty(运动的),foobar(...).可以实现鼠标莫过或者点击图片才开始加载
      
      container: $('#container'), // 对某容器中的图片实现效果
      // container,值为某容器.lazyload默认在拉动浏览器滚动条时生效,这个参数可以让你在拉动某DIV的滚动条时依次加载其中的图片
      
      failurelimit: 10  // 图片排序混乱时
      /*
        failurelimit,值为数字.lazyload默认在找到第一张不在可见区域里的图片时则不在继续加载,但当HTML容器混乱的时候可能出现可见区域内图片没加载         出来的情况,failurelimit意在加载N张可见区域外的图片,以避免出现这个问题。
      */     
      
   });
```
