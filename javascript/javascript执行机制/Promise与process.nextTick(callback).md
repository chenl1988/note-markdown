## Promise与process.nextTick(callback)

### Promise

### process.nextTick(callback)
- process.nextTick(callback)类似于node版的“setTimeout”，在事件循环Event Loop的下一次循环中调用callback回调函数


---

- 除了广义的同步和异步任务，对任务还可以进行更精细的定义：
  - macro-task（宏任务）：包括整体的script，setTimeout，setInterval
  - micro-task（微任务）：Promise,process.nextTick

- 不同的任务会进行不同的Event queue，比如setTimeout，setInterval会进行相同的Event queue