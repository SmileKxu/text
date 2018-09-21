### 对于移动端H5开发小结

1. 首先整个项目都是由H5开发(包含HTML5,CSS3以及js)，这里可以用到[animate.css](https://daneden.github.io/animate.css/)这个库。
可以快速的添加一些动画效果，从官网下载封装好的css文件引入，然后添加相对应的类名就可以出现相对应的效果。
```html
<link rel='stylesheet' href='css/animate.min.css'>
```
在引入其对应的类名的时候一定要引入一个 animated 类，若是对于无限的运动效果那么在添加一个 infinite。
[关于animate更多看github](https://github.com/daneden/animate.css);

对于翻页效果的H5页面，那么可以引入一个swiper这个库，有许多效果可以参考使用[swiper中文网](http://www.swiper.com.cn/api/index.html);

目前就暂时先用这这两个东西配合代码实现页面效果，因为页面是要适配移动端的代码，那么就需要做适配下面写出当前我知道的适配方法。

首先需要引入viewport,如下:
```
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no, minimal-ui" />
```
然后淘宝移动布局js如下:[参考链接](https://www.cnblogs.com/well-nice/p/5509589.html);
```js
// 淘宝移动端布局方法
    let scale = 1 / devicePixelRatio;
    console.log(scale);
    document.querySelector('meta[name="viewport"]').setAttribute('content', 'initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');

    console.log(scale);
    console.log(document.documentElement.clientWidth);
    document.documentElement.style.fontSize = document.documentElement.clientWidth / 10 + 'px';
```
另一种rem适配方法如下:[参考链接](https://zhuanlan.zhihu.com/p/23363538);
```js
(function(doc, win) {
        var docEl = doc.documentElement,
            resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
            recalc = function() {
                var clientWidth = docEl.clientWidth;
                console.log(docEl.clientWidth);
                if (!clientWidth) return;
                if (clientWidth >= 750) {
                    docEl.style.fontSize = '100px';
                } else {
                    docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
                }
            };

        if (!doc.addEventListener) return;
        win.addEventListener(resizeEvt, recalc, false);
        doc.addEventListener('DOMContentLoaded', recalc, false);
        console.log(document.documentElement.clientWidth);
    })(document, window);
```
然后就可以根据客户的要求来进行代码的编写以及页面的布局，大多数都是图片的动画效果。

对于苹果手机alert弹出提示带链接取消方法
```js
window.alert = function(name) {
		var iframe = document.createElement("IFRAME");
		iframe.style.display = "none";
		iframe.setAttribute("src", 'data:text/plain,');
		document.documentElement.appendChild(iframe);
		window.frames[0].window.alert(name);
		iframe.parentNode.removeChild(iframe);
	}
```


