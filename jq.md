### DOM文档的加载顺序是由上而下的顺序加载。

1. DOM加载到link标签

css文件的加载是与DOM的加载并行的，也就是说，css在加载时Dom还在继续加载构建，而过程中遇到的css样式或者img，则会向服务器发送一个请求，待资源返回后，将其添加到dom中的相对应位置中；

2. DOM加载到script标签

由于js文件不会与DOM并行加载，因此需要等待js整个文件加载完之后才能继续DOM的加载，倘若js脚本文件过大，则可能导致浏览器页面显示滞后，出现“假死”状态，这种效应称之为“阻塞效应”；会导致出现非常不好的用户体验；

而这个特性也是为什么在js文件中开头需要$(document).ready(function(){})或者（function(){}）或者window.onload,即是让DOM文档加载完成之后才执行js文件，这样才不会出现查找不到DOM节点等问题；

js阻塞其他资源的加载的原因是：浏览器为了防止js修改DOM树，需要重新构建DOM树的情况出现；

3. 解决方法

前提，js是外部脚本；

在script标签中添加 defer=“ture”，则会让js与DOM并行加载，待页面加载完成后再执行js文件，这样则不存在阻塞；

在scirpt标签中添加 async=“ture”，这个属性告诉浏览器该js文件是异步加载执行的，也就是不依赖于其他js和css，也就是说无法保证js文件的加载顺序，但是同样有与DOM并行加载的效果；

同时使用defer和async属性时，defer属性会失效；

可以将scirpt标签放在body标签之后，这样就不会出现加载的冲突了。

### 对于jquery的$(function(){})以及js中的window.onload()区分如下:

1. jquery是对DOM进行操作的，也就是说需要 DOM 结构加载完成之后，jquery才能工作，

那么 $(document).ready() 或者 $(function(){}) 的作用就是等待DOM 结构加载完成，然后再

执行里面的jquery操作；

2. js有一个 window.onload( ) ,这个的作用是等待页面上的所有资源都加载完成才执行函数里面的

代码，和jquery是有区别的。

但是，在js中，也有一个 DOMContentLoaded 事件 和 jquery 的作用是一样的；
