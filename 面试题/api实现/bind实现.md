# 手写bind()

## bind方法创建一个新的函数，在bind()被调用时，这个新函数的this被指定为bind()的第一个参数，而其余参数将作为新函数的参数，供调用时使用

  - 语法： function.bind(thisArg, arg1, arg2, ...)
  - 在用法上看，似乎是给call/apply包了一层function就实现了bind()