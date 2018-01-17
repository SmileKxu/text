### 关于 CJCC 项目门禁系统的逻辑处理

这个项目的目的是为了在其原有的刷卡系统上，增加一个profile(禁用摄像头)功能。

这个功能的实现在 airwatch 上，所以需要员工注册 airwatch 账号，这样就可以获得员工 device 的序列号。

然后建立一张包含全部员工信息的表格(包括device信息)，再员工刷卡的时候，根据其ID找到device然后根据标志位判定添加profile还是移除profile。
