## async/await

- async/await 是在 ES7 版本中引入的，它对于 javascript 中的异步编程而言是一个巨大的提升。它可以让我们以同步的方式处理异步的流程，同时不会阻塞主线程。

- async/await 函数返回一个 Promise 对象，当函数执行的时候，一旦遇到 await 就会先返回，等到触发异步操作完成，再执行函数体内后面的语句。可以理解为，是让出了线程，跳出了 async 函数体

```
async function func1() {
    return 1
}

console.log(func1()); //很显然，func1的运行结果其实就是一个Promise对象，因此可以使用then来处理后续逻辑

func1().then(res => {
    console.log(res);  // 30
})
```

- await 的含义为等待，也就是 async 函数需要等待 await 后的函数执行完成并且有了返回结果（Promise 对象）之后，才能继续执行下面的代码。await 通过返回一个 Promise 对象来实现同步的效果

- async/await 是参照 Generator 封装的一套异步处理方案，可以理解为 Generator 的语法糖

  - 所以了解就不得不了解 Generator
  - 而 Generator 又依赖于迭代器 Iterator
  - 而 Iterator 的思想来源于单向链表

### async/await 的优点

- async/await 带给我们最大的一个好处就是同步的编程风格
