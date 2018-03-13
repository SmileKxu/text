# Swiper Animate使用方法

[Swiper官网](http://www.swiper.com.cn/usage/animate/index.html)

Swiper Animate 是Swiper中文网提供的用于在Swiper内快速制作CSS3动画效果的小插件，适用于Swiper2.x、Swiper3.x和
Swiper4.x。 此插件不适用于loop模式

1. 使用Swiper Animate需要先加载swiper.animate.min.js和animate.min.css。

```html
<!DOCTYPE html>
<html>
<head>
    ...
    <link rel="stylesheet" href="path/to/swiper.min.css">
    <link rel="stylesheet" href="path/to/animate.min.css">
</head>
<body>
    ...
    <script src="path/to/swiper.min.js"></script>
    <script src="path/to/swiper.animate.min.js"></script>
</body>
</html>
```

2. 初始化时隐藏元素并在需要的时刻开始动画。
```html
 <script>
 //Swiper4.x
   let mySwiper = new Swiper('.swiper-container', {
    
      direction: 'vertical', // 纵向分屏，不加的话默认为横向
      on:{
        init: function(){
          swiperAnimateCache(this); //隐藏动画元素
          swiperAnimte(this); //初始化完成开始动画
        },
      slideChangeTransitionEnd: function(){
        swiperAnimate(this); // 每个slide切换结束时也运行当前slide动画
      }
     }
   })
 </script>
</body>
```
3. 在需要运动的元素上面增加类名 ani，和其他的类似插件相同，Swiper Animate需要指定几个参数:

swiper-animate-effect: 切换效果，例如 fadeInUp //切换效果直接去 animate.css 官网查找
swiper-animate-duration: 可选，动画持续时间(单位秒)，例如 0.5s
swiper-animate-delay: 可选，动画延迟时间(单位秒)，例如 0.3s

```html
<div class='swiper-slide'>
<p class='ani' swiper-animate-effect='fadeInUp' swiper-animate-duration='0.5s' swiper-animate-delay='0.3s'>内容</p>
</div>
```

### 使用swiper后body内的结构大致如下
```html
<body>
    <div class="swiper-container">
        <div>
            <section class='swiper-slide'>slider1</section>
            <section class='swiper-slide'>slider2</section>
            <section class='swiper-slide'>slider3</section>
        </div>
    </div>
</body>   
```
大致的代码逻辑就是这样，每一个包含swiper-slide的section标签就会是一个页面，这个标签内可以写实现动画效果的部分。


