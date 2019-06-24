## promise

- then 接收一个函数作为参数，并且会拿到 test()中调用 resolve 时传的参数
- then 里面的函数就跟平时的回调函数是一个意思，能够在 test()这个异步任务执行完成之后被执行
- 这就是 Promise 的作用了，简单来讲，就是能把原来的回调写法分离出来，在异步操作执行完后，用链式调用的方式执行回调函数

```
  function test() {
    var p = new Promise(function (resolve, reject) {
      //做一些异步操作
      setTimeout(function () {
        console.log("执行完成");
        resolve("hahaha");
      }, 2000);
    })
    return p;
  }
  test().then(function (data) {
    console.log(data);
  })
```

- Promise 的精髓是“状态” ，用维护状态、传递状态的方式来使得回调函数能够及时调用，它比传递 callback 函数要简单、灵活的多

```
/* 使用Promise的正确场景 (链式操作)*/
  test().then(data => {
    console.log(data);
    return test2();
  }).then(data => {
    console.log(data);
    return test3();
  }).then(data => {
    console.log(data);
  })
```

- Promise.all，接收一个数组参数，里面的值最终都算返回 Promise 对象，三个异步操作是并行执行的。等到它们都执行完成后才会进到 then 里面
- all 方法的效果实际上是【谁跑的慢，以谁为准执行回调】

```
  Promise.all([test(), test2(), test3()]).then(function (results) {
  console.log(results); //[ 'hahaha', 'hahaha2', 'hahaha3' ]
  })
```

- Promise.race【谁跑的快，以谁为准执行回调】，用法与 all 一样
- 使用场景，比如可以用 race 给某个异步请求设置超时时间，并且在超时后执行相应的操作

```
  Promise.race([test(), test2(), test3()]).then(function (results) {
  console.log(results);
  })
```
