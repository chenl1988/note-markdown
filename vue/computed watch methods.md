### computed watch methods 用法和区别

- computed 和 watch 自动追踪数据，执行相关函数，methods 需要手动调用
- computed 是计算属性，用法和 data 一致
- watch 像事件监听，对象发生变化时，执行相关操作
- methods 与 js 中执行方法类似
- computed 通常只有 get 属性
- 数据变化的同时进行异步操作或者是比较大的开销，那么 watch 为最佳选择
- watch 的对象必须事先声明
