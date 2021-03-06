## eventloop 事件循环

- javascript引擎并不是独立运行的，它运行在宿主环境中。所有的环境中都有一个共同的“点”（thread，也指线程），即它们都提供了一种机制来处理程序中的多个块的执行，且执行每块时调用javascript引擎，这种机制被称为事件循环。

- 换句话说javascript引擎并没有时间的概念，只是一个按需执行的javascript任意代码片段的环境，“事件”（javascript中代码执行）调度总是由包含它的环境进行。

- 举例来说，javascript程序发出一个ajax请求，从服务器获取一些数据，那就在一个函数（通常是回调函数）中设置好响应代码，然后javascript引擎会通知宿主环境：“我现在要暂停执行，你一旦完成网络请求，拿到了数据，就请调用这个函数”；然后浏览器就会设置侦听来自网络的响应，拿到要给你的数据之后，就会把回调函数插入事件循环，以此来实现这个回调的调度执行。

- eventloop是一个用作队列的数组 （先进先出）

```
//事件循环的简化伪代码

var eventloop = [];
var event;
//while循环实现的持续运行的循环
while(true){
  //一次tick 对于每次tick而言，如果队列中有等待的事件，那么就会从队列中摘下一个事件并执行，
  if(eventloop.length>0){
    event = eventloop.shift();
    try{
      event();
    }catch(err){
      reportError(err);
    }
  }
}
```
- setTimeout(..)并没有把你的回调函数挂在事件循环队列中，它所做的是设定一个定时器，当定时器到时后，环境会把你的回调函数放在事件循环中，这样，在未来的某个时刻的tick会摘下并执行这个回调

- 程序通常被分成了很多小块，在事件循环中一个接一个地去执行，严格的说，和你的程序不直接相关的其他事件也可能会插入到队列中

---

- ES6从本质上改变了在哪里管理事件循环，这意味着事件循环不再只由宿主环境；这个改变的主要原因是ES6中Promise的引入，因为这项技术要求对事件循环队列的高度运行能够直接进行精细控制