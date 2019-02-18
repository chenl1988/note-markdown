## javascript 中的 Function 和 Object

- js中一切皆对象
- js 中所有的对象都继承自 **Object 原型**（包括函数、内置对象[Array,String...]），而 Function 充当了 Object 的构造器；
- Object 和 Function 都既是函数也是对象。
- 由 new + function 构造器（new Foo()）实例化出来的对象不是函数，仅仅是 Object 的子类
- 所有的对象都有一个 Function 的构造器存储在该对象原型链的 constructor 属性中
- Function 是一个顶级函数，所有的函数都是 Function 的子类，包括内置的函数（内置的对象）和通过自定义的 function 关键字定义的函数
- Function.prototype 原型链上的属性共享给所有函数
- Object.prototype 原型链上的属性共享给所有对象
