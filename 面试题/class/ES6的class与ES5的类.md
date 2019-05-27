## ES6 中的 class 和 ES5 的类有什么区别？

- ES6 class 内部所有定义的方法都是不可枚举的；
- ES6 class 必须使用 new 调用
- ES6 class 不存在变量提升
- ES6 class 默认都是严格模式
- ES6 class 子类必须在父类的构造函数中调用 super()，这样才有 this 对象；ES5 中的类继承的关系是相反的，先有子类的 this，然后用父类的方法应用在 this 上。
