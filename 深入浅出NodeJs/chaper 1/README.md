# Node简介

##  1.Node的特点
### 1.1 异步I/O
Don‘t tell me, I will call you的原则。－> 等待回调。
### 1.2 事件与回调函数
request中的`data`， `end`事件
```javascript
//接受中
req.on('data', function()) {

};
//接受完毕
req.on('end', function()) {

};
```
### 1.3 单线程
保持了JS单线程的特点。没有死锁。
但是缺点有：
* 无法利用多核CPU。
* 错误会引起整个应用退出。
* 大量计算占用CPU会导致无法继续调用异步I／O。
HTML5种定制了Web workers的标准来解决大计算阻塞UI渲染的问题，将计算量分发到工作线程，通过消息传递的方式将结果传递给主线，从而不阻塞住县城。
但是这也使得工作线程不能访问UI线程。
Node使用了同样的方法来解决大计算量的问题：`child_process`!!!

### 1.4 多平台

## 2. 应用场景
### 2.1 I/O密集型
I/O密集的优势，主要在于Node利用时间循环的处理能力，而不是启动每一个线程为每一个请求服务，资源占用极少。
### 2.2 是否不删成CPU密集型服务
V8的执行效率极高。
主要挑战：由于JS单线程的原因，如果有长时间运行的计算，将会导致CPU时间片不能释放，使得后续的I／O无法发起。
但是调整和分解运算任务为多个小任务就可以适时释放，不阻塞I／O调用！！！
