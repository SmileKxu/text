### window.open
根据指定的参数，将一个资源加载到一个新的浏览上下文(如一个窗口)或一个已经存在的浏览上下文中。

### 语法
```js
let windowObjetReference = window.open(strUrl, strWindowName, [strWindowFeatures]);

/*
strUrl === 要在新打开的窗口中加载的URL。
strWindowName === 新窗口的名称。
strWindowFeatures === 一个可选参数，列出新窗口的特征(大小，位置，滚动条等)作为一个DOMString。
*/
```
### 参数与返回值
WindowObjectReference <br>
打开的新窗口对象的引用。如果调用失败，返回值会是null。如果父子窗口满足同源策略，可以通过这个引用访问新窗口的属性和方法。

strUrl <br>
新窗口需要载入的url地址。strUrl可以是web上的html页面也可以是图片文件或者其他任何浏览器支持的文件格式。

strWindowName <br>
新窗口的名称。该字符串可以用来作为超链接<a>活表单<form>元素的目标属性值。字符串种不能含有空白字符。 <br>
注意: strWindowName 并不是新创口的标题。

strWindowFeatures <br>
可选参数。是一个字符串值，这个值列出了将要打开的窗口的一些特性(窗口功能和工具栏)。字符串种不能包含任何空白字符，
特性之间用逗号分隔开。参考下文的位置和尺寸特征。

### 说明

open()方法，创建一个新的浏览器窗口对象，如同使用文件菜单中的新窗口命令一样。strUrl参数制定了该窗口将会打开的
地址。如果strUrl是一个空值，那么打开的窗口将会是带有默认工具栏的空白窗口(加载about:blank)。

注意：调用window.open()方法以后，远程URL不会被立即载入，载入过程是异步的。(实际加载这个URL的时间推迟到当前脚本块
执行结束之后。窗口的创建和相关资料的加载异步地进行)。
