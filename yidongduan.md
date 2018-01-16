### PC端代码适配移动端方法

对于PC端的页面如果想放在移动端(微信等)，直接打开那么页面的尺寸不是适配的，依旧是按照PC的设置。想要适配需要引入一下meta标签
```
<meta http-equiv="X-UA-Compatible" content="IE=edge"/>
<meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0" name="viewport">
<meta content="yes" name="apple-mobile-web-app-capable">
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<meta content="telephone=no" name="format-detection">
```

1. 设置浏览器的兼容模式(让IE使用最新的浏览器渲染)
```
<meta http-equiv="X-UA-Compatible" content="IE=edge"/>
```
2. 视口，将页面容器缩放到设备大小展示
```
<meta content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=0" name="viewport">
```
3. 删除默认的苹果工具栏和菜单栏
```
<meta content="yes" name="apple-mobile-web-app-capable">
```
4. 控制状态栏显示样式
```
<meta content="black" name="apple-mobile-web-app-status-bar-style">
```
5. 禁止将页面中一连串数字识别为电话号码、并设置为手机可以拨打的一个连接。(这个标签的默认值 telephone=yes)
```
<meta content="telephone=no" name="format-detection">
```
