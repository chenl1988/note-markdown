## async/await

- async/await 是在 ES7 版本中引入的，它对于 javascript 中的异步编程而言是一个巨大的提升。它可以让我们以同步的方式处理异步的流程，同时不会阻塞主线程。

- async/await 函数返回一个 Promise 对象，当函数执行的时候，一旦遇到 await 就会先返回，等到触发异步操作完成，再执行函数体内后面的语句。可以理解为，是让出了线程，跳出了 async 函数体

- async/await 是参照 Generator 封装的一套异步处理方案，可以理解为 Generator 的语法糖

  - 所以了解就不得不了解 Generator
  - 而 Generator 又依赖于迭代器 Iterator
  - 而 Iterator 的思想来源于单向链表

```
function testAwait(){
   return new Promise((resolve) => {
       setTimeout(function(){
          console.log("testAwait");
          resolve();
       }, 1000);
   });
}
 
async function helloAsync(){
   await testAwait(); //await返回的是一个promise对象
   console.log("helloAsync");
 }
helloAsync();
// testAwait
// helloAsync
```

### await

- await 的含义为等待，也就是 async 函数需要等待 await 后的函数执行完成并且有了返回结果（Promise 对象）之后，才能继续执行下面的代码。await 通过返回一个 Promise 对象来实现同步的效果

- await操作符用于等待一个Promise对象，它只能在异步函数async function 内部使用

- `[return_value] = await expression;`： expression：一个promise对象或者任何要等待的值

- await针对所跟不同表达式的处理方式：

	- Promise对象：await会暂停执行，等待Promise对象resolve，然后恢复async函数的执行并返回解析值
	- 非Promise对象：直接返回对应的值

### 返回值

- 返回Promise对象的处理结果。如果等待的不是Promise对象，则返回该值本身

- 如果一个Promise被传递给一个await操作符，await将等待Promise正常处理完成并返回其处理结果

```
function testAwait (x) {
  return new Promise(resolve => {
    setTimeout(() => {
      resolve(x);
    }, 2000);
  });
}
 
async function helloAsync() {
  var x = await testAwait ("hello world");
  console.log(x); 
}
helloAsync ();
// hello world
```

- 正常情况下，await命令后面是一个Promise对象，它也可以跟其他值，如字符串，布尔值，数值以及普通函数
```
function testAwait(){
   console.log("testAwait");
}
async function helloAsync(){
   await testAwait();
   console.log("helloAsync");
}
helloAsync();
// testAwait
// helloAsync
```

### async/await 的优点

- async/await 带给我们最大的一个好处就是同步的编程风格
