#### form表单

在HTML中，form标记被用于定义表单域，即创建一个表单。
form是一个双标签，其具体属性有action method和name。
action: 属性用于指定接受和处理表单数据服务器程序的url地址。
methed: 属性用于设置表单数据的提交方式，取值为get或post。
name: 属性用于指定表单的名称，用于区分同一个页面的多个表单。

form 表单中 input标签的基本语法格式:
<input type="input类型" .../> type属性为最基本的属性 指定不同的控件类型
一般type类型为以下几种:
1. text           单行文本输入框
2. password       密码输入框
3. radio          单选按钮
4. checkbox       复选框
5. button         普通按钮
6. submit         提交按钮
7. reset          重置按钮
8. hidden         隐藏域
9. file           文件域

还有许多Boolean属性的属性值
1. readonly       该控件内容为只读(不能编写修改)
2. checked        定义选择控件默认被选中的项
3. maxlength      控件允许输入的最多字符数
4. disabled       第一次加载页面时禁用该控件(显示为灰色)

对于file文件域 accept用于选择文件类型 默认一次只能选择一个 设置multiple可以选择多项

textarea也属于form表单内的标签，

在jquery代码中 return false; 可以阻止表单上传。

表单事件：

.focus() 与 .blur() 的效果为获得焦点或者失去焦点

.submit() 事件 可以在表单数据发送时截取数据不让数据发送 判断数据是否书写正确
输入 return false; 就可以阻止表单数据提交。

.change() 事件 在元素失去焦点时候将触发change事件。

对于<input> 标签来说 $(this).val() 获取的是其内容

对于<select> 标签内的 <option> 标签来说 $(this).val()获得的是<option>标签所设置的
value值。在<select> .change()事件的函数中，要填写event获取。
 
获取radio 和 checkbox 的值要使用 checked获取 使用时要在选到的类后面接 :checked就可以

console.log() 可以打印变量结果 与其结果相似的还有 console.info() 和 console.error();

在使用event.data()的时候，要在一个for循环里，将迭代变量i的值传递给on()方法，保留当前迭代
的值，也就是在事件的函数前面先传入一个i 然后, 接function如下
 $("button").eq(i).click(i, function(){ });
 
对于 input 和 textarea 标签，可以注册 oninput事件和onchange事件，oninput 事件在元素值发生变化是立即触发， onchange 在元素失去焦点时触发，
selector标签也可以注册 onchange事件。
