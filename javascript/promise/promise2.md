## Promise

- Promise 就是一个代表了异步操作最终完成或者失败的结果对象
- Promise 本质上是一个绑定了回调的对象，而不是将回调传进函数内部
- 基本上 Promise 还是有点像事件回调的，除了:
  - 一个 Promise 只能成功或失败一次，并且状态无法改变（不能从成功变为失败，反之亦然）
  - 如果一个 Promise 成功或者失败之后，为其添加针对成功/失败的回调，则相应的回调函数会立即
- 一个 Promise 的状态可以是：

  - 确认（fulfilled） 成功
  - 否定（rejected） 失败
  - 等待（pending） 还没有确认或者否定，进行中
  - 结束（settled） 已经确认或者否定了

- Promise 的构造器接受一个函数作为参数，它会传递给这个回调函数两个变量 resolve 和 reject。在回调函数中做一些异步操作，成功之后调用 resolve，否则调用 reject

```
var promise = new Promise(function(resolve, reject) {
  // do a thing, possibly async, then…

  if (/* everything turned out fine */) {
    resolve("Stuff worked!");
  }
  else {
    reject(Error("It broke"));
  }
});


promise.then(function(result) {
  console.log(result); // "Stuff worked!"
}, function(err) {
  console.log(err); // Error: "It broke"
});
```

- then 接受两个参数，成功的时候调用一个，失败的时候调用另一个，两个都是可选的，所以可以只处理成功或失败的情况
