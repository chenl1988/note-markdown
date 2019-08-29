## Pormise

- 在 javascript 中，所有代码都是单线程执行的（这意味着任何两句代码都不能同时运行），由于这个“缺陷”，导致 JavaScript 的所有网络操作，**浏览器事件，都是异步执行的，异步执行可以用回调函数实现**：

- Promise 本身是同步的立即执行函数，在 executor 中执行 resolve 或者 reject 的时候，此时是异步操作，会先执行 then/catch 等，当主栈完成后，才会去调用 resolv/reject 中存放的方法执行。

- promise1 是 resolved 或 rejected: 这个 task 就会放入当前事件循环回合的 microtask queue（微任务）；而 setTimeout 的回调也是个 task，会被放入 macrotask queue（宏任务），即使是 0ms 的情况

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

- 异步操作会在将来的某个时间点触发一个函数调用

- Pormise 有各种开源实现，在 ES6 中被统一规范，由浏览器直接支持

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

- **可见 Promise 的最大好处是在异步执行的流程中，把执行代码和处理结果的代码清晰的分离了**

- Promise 不论成功或失败都会调用 then()然而 catch()只有当 promise 失败时才会调用

- Promise 还可以做更多的事情，比如，有若干个异步任务，需要先做任务 1，如果成功后再做任务 2，任何任务失败则不再继续并执行错误处理函数；要串行多个任务，不用 Promise 需要写一层一层的嵌套代码，有了 Promise，只需要简单的写:

```
job1.then(job2).then(job3).catch(handleError);
//其中job1、job2、job3都是Promise对象
```

- Promise 还可以并行执行异步任务，用 Promise.all()实现

- 有时多个异步任务为了容错，比如同时向两个 URL 读取用户的个人信息，只需要获取先返回的结果即可，这种情况可以用 Promise.race()实现
