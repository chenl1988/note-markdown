## 改变函数内部 this 指针的指向函数（bind，apply，call 的区别）

- 执行函数并将 this 的指向进行修改

- 通过 call 和 apply 改变函数的 this 指向，这两个函数的第一个参数都是一样的，表示要改变指向的那个对象，第二个参数，apply 是数组，而 call 则是 arg1,arg2...这种形式。

- 通过 bind 改变 this 作用域会返回一个新的函数，这个函数不会马上执行

---

- call,apply,bind 都是用来改变函数执行时上下文，可借它们实现继承
- call 和 apply 唯一区别是参数不一样，call 是 apply 的语法糖
- bind 是返回一个新函数，供以后调用
