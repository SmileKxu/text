## 1.node.js 的优缺点，针对缺点的解决方案

#### 优点:
1.采用事件驱动、异步编程、利用JavaScript的匿名函数和闭包特性，专门为网络服务而设计。<br>
2.在运行效率方面: node.js 非阻塞模式的 I/O 处理给 node.js 带来相对低系统资源耗用下的高性能和出众的负载能力。<br>
3.node.js 轻量高效，对于数据密集型分布式部署环境下的实时应用系统具有完美的解决方案。

#### 缺点:
1.可靠性低。<br>
2.node.js 是单线程，单进程，运行在单核 CPU 上，不能充分利用多核 CPU，一旦这个进程失去响应，那么整个 web 服务器都将崩溃。 <br>

#### node.js 的网络服务器支持多进程的方案
1.开启多个进程，并绑定到不同的端口监听，使用反向代理服务器做负载均衡。<br>
2.多个进程绑定到同一个端口监听，通过 node.js 可以在不同进程中发送文件句柄来进行通信。
<hr>

## 2.node.js 的事件循环机制
node.js 程序由事件循环开始，到事件循环结束，所有的逻辑都是事件的回调函数，所以 node.js 始终在事件循环中，程序入口就是循
环第一个事件的回调函数。事件的回调函数在执行的过程中，可能会发出 I/O 请求或直接发射 (emit)事件，执行完毕后再返回事件循环，
事件循环会检查事件队列中有没有未处理的事件，直到程序结束。

## 3.同步和异步是什么
同步: 当一个调用发出后，调用不会立即返回直到得到调用结果。<br>
异步: 当一个调用发出后，调用者线程不需要等待调用结果的返回就可以继续执行后续操作，实际处理调用的操作会以
状态或者消息来通知调用口，或者通过已定的回调函数来处理调用结果。

## 4.node.js 常用的全局变量
console, process, Buffer, global, __filename(当前绝对路径下文件名)，__dirname(当前文件绝地哦路径目录) 
global:最根本的作用是为全局变量的宿主，表示 Node 所在的全局环境。<br>
process:该对象表示 Node 所处的当前进程，允许开发者与该进程互动。<br>
console:指向 Node 内置的 console 模块，提供命令行环境中的标准输入、标准输出功能。


## 5.node.js 的核心模块
http, fs(文件系统), exent(事件), Stream(流), URL, QueryString, Path, child_process

## 6.props 和 state 的区别
props 是属性，state 是状态，两者都是 React 组件对象，都是组件对象存储和传递数据的载体。<br>
props: props大多数组件在定义时就可以通过各种自定义参数来实现组件的定制。对外提供的这些参数就成为 props。<br>
state: 作为用户交互设计产生的反馈通常都是 state 来进行数据的改变，界面的刷新。<br>
props(作用):一般用于父组件像子组件通信，在组件之间通信使用。<br>
state(作用):一般用于组件内部的状态维护，更新组件内部的数据，状态，更新子组件的props等。<br>

## 7.node.js 的整体架构
node.js 在整体上分为三部分: 应用app >> v8 和node.js内置架构 >> 系统在上述的中间环节又分为三层:<br>
1. javascript 实现的核心模块<br>
2. c++ 绑定(socket, http, fs, ...)<br>
3. v8(node 的绑定)，asyncI/O(libuv),EventLoop(libuv)

## 8.React 组件的生命周期
React 组件的生命周期在大的方面分为三部分: mount， update， unmount <br>
1.mount部分: 组件第一次渲染过程: constructor(组件的构造函数)，getInitialState(设置初始状态属性)，componentWillMount,
mounting,componentDidMount。<br>
2.update部分: 改变state 后组件的更新过程:componentReciveProps，shouldComponentUpdate(是否执行本次更新 true/false)，
componentWillUpdate，updating，componentDidUpdate。<br>
3.unmount部分: 移除组件过程:componentWillUnmount，unmounting。<br>

## React 的实现原理
React是以组件的形式构建页面上的 DOM，并将组件构建为一种状态机，组件的形式是由状态属性决定，状态的属性是组件形式的数据表现。<br>

React组件在加载时，会根据初始的状态属性通过render方法先构建组件的虚拟DOM，在将虚拟DOM渲染到页面中，所以首次加载页面是会慢一些
当行为改变组件状态属性state时，React会生成当前状态对应下的虚拟DOM，并和前一次的虚拟DOM进行diff算法，得到需要改变的DOM，最后将这
部分改变的DOM更新到实际的DOM中。<br>

## Redux 的实现原理
Redux 中主要由三部分组成: Action,Reducer,Store。<br>
Action 用来传递操作 state的信息到store，是store的唯一来源。<br>
Reducer 用来处理 action，通过传入旧的 state 和 action 来指明如何更新state。<br>
action 用来描述发生了什么，reducer 根据 action 更新 state，Store 就是把这几样东西连接到一起的对象。<br>

首先用户发出Action，然后 Store 自动调用Reducer，并且传入两个参数:当前 State 和收到的 Action。Reducer 会返回新的
State。State 一旦有变化，就会重新渲染组件。








