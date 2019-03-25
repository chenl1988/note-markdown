## other

```
function Foo(){}
var a = new Foo();
```

- isPrototypeOf()：只要是原型链里中出现的原型，就会返回true
  -`Foo.prototype.isPrototypeOf(a);` 在a 的整条原型链中是否出现过Foo.prototype
- Object.getPrototypeOf():直接获取一个对象的`[[prototype]]`链
  `Object.getPrototypeOf(a) === Foo.prototype`

- 如果要访问对象中并不存在的一个属性，`[[Get]]`操作就会查找对象内部`[[Prototype]]`关联的对象。这个关联关系实际上定义了一条“原型链”，在查找属性时会对它进行遍历

---

- 虽然javascript中的机制和传统面向类语言中的“类初始化”和“类继承”很相似，但是JavaScript中的机制有一人核心的区别，那就是不会进行复制，对象之间是通过内部的`[[Prototype]]`链关联的。

---

- 在 es6 中引入了关键字 class，但是只是语法糖，javascript 仍然是基于原型的

---

- 所有实例都是对象，但是所有对象不一定是实例
- 每个实例对象都是通过 new 操作符创建的


