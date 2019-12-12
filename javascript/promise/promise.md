## Pormise

- 异步操作会在将来的某个时间点触发一个函数调用

- 在 javascript 中，所有代码都是单线程执行的（这意味着任何两句代码都不能同时运行），由于这个“缺陷”，**导致 JavaScript 的所有网络操作，浏览器事件，都是异步执行的，异步执行可以用回调函数实现**：

- Promise 本身是同步的立即执行函数，在 executor（执行器） 中执行 resolve 或者 reject 的时候，此时是异步操作，会先执行 then/catch 等，当主栈完成后，才会去调用 resolv/reject 中存放的方法执行。

- Pormise 有各种开源实现，在 ES6 中被统一规范，由浏览器直接支持

### Promise-微任务

- promise1 是 resolved 或 rejected: 这个 task 就会放入当前事件循环(Event Loop)回合的 microtask queue（微任务）；而 setTimeout 的回调也是个 task，会被放入 macrotask queue（宏任务），即使是 0ms 的情况

  - macro-task(宏任务)：包括整体代码 script，setTimeout，setInterval
  - micro-task(微任务)：Promise，process.nextTick

  ```
  function callback() {
    console.log("Done");
  }
  console.log("before setTimeout()");
  setTimeout(callback, 1000);
  console.log("after setTimeout()");

  //before setTimeout()
  //after setTimeout()
  //(等待1秒后)
  //Done
  ```
- 特性：promise 对象的错误具有冒泡的性质，会一直向后传递，直到被捕获为止，也即是说，错误总会被下一个 catch 语句捕获

### Promise状态

- Promise 的精髓是“状态” ，用维护状态、传递状态的方式来使得回调函数能够及时
调用，它比传递 callback 函数要简单、灵活的多

- 一个 Promise 的状态可以是：

  - 确认（fulfilled） 成功 resolve
  - 否定（rejected） 失败 reject
  - 等待（pending） 还没有确认或者否定，进行中
  - 结束（settled） 已经确认或者否定了

- resolve方法可以将pending转为fulfilled，reject方法可以将pending转为rejected。

### Promise作用

- 简单来讲，Promise作用就是能把原来的回调写法分离出来，在异步操作执行完后，用链式调用的方式执行回调函数

- **可见 Promise 的最大好处是在异步执行的流程中，把执行代码和处理结果的代码清晰的分离了**

- Promise 不论成功或失败都会调用 then()，然而 catch()只有当 promise 失败时才会调用

- **Promise 本质上是一个绑定了回调的对象，而不是将回调传进函数内部**

- 基本上 Promise 还是有点像事件回调的，除了:
  - 一个 Promise 只能成功或失败一次，并且状态无法改变（不能从成功变为失败，反之亦然）
  - 如果一个 Promise 成功或者失败之后，为其添加针对成功/失败的回调，则相应的回调函数会立即

```
/*
  test函数有两个参数，这两个参数都是函数，如果执行成功会调用resolve()，如果执行失败会调用reject()
  可以看出，test()只关心自己的逻辑，并不关心具体的resolve和reject将如何处理结果
  */
function test(resolve, reject) {
  var timeOut = Math.random() * 2;
  console.log(`set timeout to ${timeOut} seconds`);
  setTimeout(function () {
    if (timeOut < 1) {
      console.log("call resolve()...");
      resolve("200 ok");
    } else {
      console.log("call reject()...");
      reject(`timeout in ${timeOut} seconds...`);
    }
  }, timeOut * 1000)
}

/*
有了执行函数，可以用一个Promise对象来执行它，并在将来的某个时候获得成功或失败的结果
p1 是一个Promise对象，它负责执行test函数。test函数内部是异步执行的
*/
var p1 = new Promise(test);
var p2 = p1.then(function (result) {
  console.log(`成功: ${result}`);
})
var p3 = p2.catch(function (reason) {
  console.log(`失败: ${reason}`);
})

/* Promise对象可以串联起来，所以可以简化为： */
new Promise(test).then(function (result) {
  console.log(`成功：${result}`);
}).catch(function (reason) {
  console.log(`失败：${reason}`);
});
```
### Promise链式调用

- Promise 还可以做更多的事情，比如，有若干个异步任务，需要先做任务1，如果成功后再做任务2，任何任务失败则不再继续并执行错误处理函数；要串行多个任务，不用 Promise 需要写一层一层的嵌套代码，有了 Promise，只需要简单的写:

```
let readFile = require('fs').readFile; // 加载node内置模块fs 利用readFile方法异步访问文件
function getFile(url){  // 创建一个读取文件方法
    return new Promise(function(resolve, reject){  // 返回一个Promise对象
        readFile(url, 'utf8', function(err,data){  // 读取文件  
            resolve(data)  // 调用成功的方法
        })
    })
}
getFile('1.txt').then(function(data){  // then方法进行链式调用
    console.log(data)  // 2.txt
    return getFile(data)    //拿到了第一次的内容用来请求第二次
}).then(function(data){
    console.log(data)  // 3.txt
    return getFile(data)  //拿到了第二次的内容用来请求第三次
}).then(function(data){
    console.log(data)  // 完成
})

```

- 每一个then方法都会返回一个新的Promise实例，让then方法支持链式调用，并可以通过返回值将参数传递给下一个then

### Promise.all()和Promise.race()

- Promise 还可以并行执行异步任务，用 Promise.all()实现（统一处理多个Promise）

- **有时多个异步任务为了容错，比如同时向两个 URL 读取用户的个人信息，只需要获取先返回的结果即可，这种情况可以用 Promise.race()实现**

- Promise.all，接收一个数组参数，里面的值最终都算返回 Promise 对象，三个异步操作是并行执行的。等到它们都执行完成后才会进到 then 里面
- all 方法的效果实际上是【谁跑的慢，以谁为准执行回调】

```
let Promise1 = new Promise(function(resolve, reject){})
let Promise2 = new Promise(function(resolve, reject){})
let Promise3 = new Promise(function(resolve, reject){})

let p = Promise.all([Promise1, Promise2, Promise3])

p.then(funciton(){
  // 三个都成功则成功  
}, function(){
  // 只要有失败，则失败 
})

```

- Promise.race【谁跑的快，以谁为准执行回调】，用法与 all 一样
- 使用场景，比如可以用 race 给某个异步请求设置超时时间，并且在超时后执行相应的操作

```
  Promise.race([test(), test2(), test3()]).then(function (results) {
  console.log(results);
  })
```
