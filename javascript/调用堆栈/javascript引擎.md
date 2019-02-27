## javascript 引擎

- javascript 引擎最流行的是谷歌的 V8 引擎，V8 引擎使用在 Chrome 以及 node 中
- 引擎主要由两部分组成：
  - 内存堆：这是内存分配发生的地方
  - 调用栈：这是代码执行时的地方
- 有些 API 经常使用到的（setTimeout）,并不是引擎提供的；一部分是由浏览器提供的 Web API,比如 DOM、AJAX、setTimeout 等；另外还有流行的事件循环和回调队列。
