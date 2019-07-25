## setInterval

- 与setTimeout()差不多，只不过setInterval是循环执行。对于执行顺序来说，setInterval()会每隔指定的时间将注册的函数置入到Event queue。如果前面的任务耗时太久，那么同样需要等待

- 需要注意的是，对setInterval(fn,ms)来说，我们已经知道不是每过ms秒会执行一次fn，而是每过ms秒，会有fn进行Event Queue。一旦setInterval()的回调函数fn执行时间超过了延迟时间ms，那么就完全看不出时间间隔了。