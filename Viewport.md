# HTML meta viewport属性说明(mark)

## 什么是Viewport
手机浏览器是把页面放在一个虚拟的'窗口' (viewport)中，通常这个虚拟的'窗口'(viewport)比屏幕宽，
这样就不用把每个网页挤到很小的窗口中(这样会破坏没有针对手机浏览器优化的网页布局)，用户可以通过
平移和缩放来看网页的不同部分。移动版的Safari浏览器最新引进了viewport这个meta标签，让网页开发者
来控制viewport的大小和缩放，其他手机浏览器也基本支持。

## Viewport 基础
一个常用的针对移动网页优化过的页面的 viewport meta 标签大致如下:
```html
<meta name='viewport' content='width=device-width, initial-scale=1, maximum-scale=1'>
```
width: 控制 viewport 的大小，可以指定的一个值，如果600，或者特殊的值，如device-width为设备的宽度(单位为缩放为100%时的CSS的像素)。
height: 和 width 相对应，指定高度。
initial-scale: 初始缩放比例，也即是当页面第一次 load 的时候缩放比例。
maximum-scale: 允许用户缩放到的最大比例。
minimun-scale: 允许用户缩放到的最小比例。
user-scalable: 用户是否可以手动缩放

## 关于viewport适配移动端设置
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>
```
这段代码的意思是，让viewport的宽度等于物理设备上的真实分辨率，不允许用户缩放。一般主流的webapp
都是这么设置的，它的作用其实是故意舍弃viewport，不缩放页面，这样dpi肯定和设备上的真实分辨率是一样的，
不做任何缩放，网页会因此显得更高细腻。

[viewport相关链接](https://www.cnblogs.com/pigtail/archive/2013/03/15/2961631.html)
