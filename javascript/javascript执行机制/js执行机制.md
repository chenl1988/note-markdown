## js执行机制

- js是单线程语言，多线程（Web-Worker）都是用单线程模拟出来的。js任务需要按顺序执行，但如果一个任务耗时过长，后一个任务也必须等着，所以将任务分为两类：
  - 同步任务
  - 异步任务

  - 例：当打开网站时，网页渲染过程就是一大堆同步任务，比如页面骨架和页面元素的渲染。而像加载图片音乐之类占用资源大、耗时久的任务就是异步任务。

![](./js执行机制.jpg)

- 导图要表达的内容用文字来表述的话：

  - 同步和异步任务分别进入不同的执行"场所"，同步的进入主线程，异步的进入Event Table并注册函数。
  - 当指定的事情完成时，Event Table会将这个函数移入Event Queue。
  - 主线程内的任务执行完毕为空，会去Event Queue读取对应的函数，进入主线程执行。
  - 上述过程会不断重复，也就是常说的Event Loop(事件循环)。

- js引擎存在montoring process进程，会持续不断的检查主线程执行栈是否为空，一旦为空，就会去Event Queue那里检查是否有等待被调用的函数

```
setTimeout(function(){
  console.log("定时器开始啦");
})

new Promise(function(resolve){
  console.log("马上执行for循环啦");
  for(var i=0;i<10000;i++){
    i==99 && resolve();
  }
}).then(function(){
  console.log("执行then函数啦");
})
console.log("代码执行结束");
/* 
马上执行for循环啦
代码执行结束
执行then函数啦
定时器开始啦
*/

let data = [];
$.ajax({
    url:www.javascript.com,
    data:data,
    success:() => {
        console.log('发送成功!');
    }
})
console.log('代码执行结束');

/*
上面是一段简易的ajax请求代码：

  - ajax进入Event Table，注册回调函数success。
  - 执行console.log('代码执行结束')。
  - ajax事件完成，回调函数success进入Event Queue。
  - 主线程从Event Queue读取回调函数success并执行。
*/

```

### setTimeout

- 这个函数是经过指定时间后，把要执行的任务加入到Event Queue中，又因为是单线程任务要一个一个执行，如果前面的任务需要的时间太久，那么只能等着，导致真正的延迟时间远远大于3秒
```
setTimeout(()=>{
  task()
},3000)

sleep(100000000);
```

- setTimeout(fn,0); 含义是，指定某个任务在主线程最早可得的空闲时间执行，意思就是不用再等多少秒了，只要主线程执行栈内的同步任务全部执行完成，栈为空就马上执行。

### setInterval

- setInterval是循环的执行，对于执行顺序来说，setInterval会每隔指定的时间将注册的函数置入Event Queue，如果前端的任务耗时太久，那么同样需要等待；每过ms秒，会有fn进入Event Queue。一旦setInterval的回调函数fn执行时间超过了延迟时间ms，那么就完全看不出来有时间间隔了。

### Promise与process.nextTick(callback)

- process.nextTick(callback)类似node.js版的“setTimeout”在，在事件循环的下一次循环中调用callback回调函数。

- 除了广义的同步任务和异步任务，对任务还有更精细的定义：
  - **macro-task(宏任务)：包括整体代码script,setTimeout,setInterval**
  - **micro-task(微任务)：Promise，process.nextTick**
- 不同类型的任务会进入对应的Event Queue，比如setTimeout和setInterval会进入相同的Event Queue

- 事件循环的顺序，决定js代码的执行顺序。进入整个代码（宏任务）后，开始第一次循环。接着执行所有的微任务。然后再次从宏任务开始，找到其中一个任务队列执行完毕，再执行所有的微任务。

```
setTimeout(function() {
    console.log('setTimeout');
})

new Promise(function(resolve) {
    console.log('promise');
}).then(function() {
    console.log('then');
})

console.log('console');

- 1、这段代码作为宏任务，进入主线程。
- 2、先遇到setTimeout，那么将其回调函数注册后分发到宏任务Event Queue。
- 3、接下来遇到Promise，new Promise立即执行，then函数被分发到微任务Event Queue
- 4、遇到console.log()立即执行
- 5、整体代码script作为第一个宏任务执行结束，看看有哪些微任务？我们发现then在微任务Event Queue里面，执行
- 6、第一轮事件循环结束了，开始第二轮循环，当然要从宏任务Event Queu开始。发现宏任务Event Queue中setTimeout对应的回调函数，立即执行
- 7、结束

- 代码首先执行宏任务，在宏任务中发现异步函数（setTimeout或setInterval），会将其回调函数注册到宏任务的Event Queue中；发现Promise的then或process.nextTick会将其分发到微任务的Event Queue中；宏任务执行一轮后会检查微任务中的代码，在Event Queue发现then或process.nextTick会执行；然后再进入到宏任务中Event Queue中，发现setTimeout的回调函数，执行。
```

### 总结

- 我们从最开头就说javascript是一门单线程语言，不管是什么新框架新语法糖实现的所谓异步，其实都是用同步的方法去模拟的，牢牢把握住单线程这点非常重要。

- 事件循环Event Loop是js实现异步的一种方法，也是js的执行机制

- javascript的执行的运行有很大的区别，javascript在不同环境下，比如node，浏览器，Ringo等等，执行方式是不同的。而运行大多指javascript解析引擎，是统一的。

- javascript是一门单线程的语言
- Event Loop是javascript的执行机制