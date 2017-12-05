## node.js定时任务: node-schedule的使用
```
安装 npm install node-schedule
```

### 使用方法
1. 确定时间
例如: 2014年2月14日，15:40执行
```
var schedule = require('node-schedule');
var date = new Date(2014,2,14,15,40,0);
var j = shcedule.scheduleJob(date, function(){
      console.log('执行任务');          
});
```
### 取消任务
```
j.cancel();
```
2. 每小时的固定时间
例如: 每小时的40分钟执行
```
var rule = new schedule.RecurrenceRule();
rule.minute = 40;
var j = schedule.scheduleJob(rule, function(){
     console.log('执行任务');   
});
```
3. 一个星期的某些天的某个时刻执行
例如: 周一到周日的20点执行
```
var rule = new schedule.RecurrenceRule();
rule.dayOfWeek = [0, new schedule.Range(1,6)];
rule.hour = 20;
rule.minute = 0;
var j = schedule.schedulJob(rule, function(){
    console.log('执行任务');
});
```
4. 没秒执行
```
var rule = new schedule.RecurrenceRule();
var times = [];
for (var i = 1, i < 60, i++){
    times.push(i);
}
rule.second = times;
var c = 0;
var j = schedule.scheduleJob(rule, function(){
    c++;
    console.log(c);
});
```
