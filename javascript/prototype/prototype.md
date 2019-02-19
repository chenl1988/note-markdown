## prototype

- prototype 是一个显式的原型属性
- 每个函数创建的时候都会默认创建一个 prototype 属性，prototype 属性指向函数的原型对象，只有函数对象才拥有 prototype 属性
- prototype 属性的值是一个对象，其中有 constructor（构造函数）和`__proto__`属性
  - constructor 解决了对象识别问题，即可以通过该属性判断出实例是哪个构造函数创建的
  - `__proto__` 每个实例都有一个`__proto__`属性，指向构造函数的原型对象，构造函数的原型对象它本身也一个实例，所以它的内部会有一个`__proto__`属性
- 使用原型（prototype）的好处是可以让所有对象实例共享它所包含的属性和方法

---

- Object.prototype 这个对象是引擎自己创建的
- Function.prototype 也是引擎创建的，并且通过**proto**将两者联系起来（即`Function.prototype.__proto__.constructor: function Object()`）
- 先有了 Function.prototype 才有的 function Function()
- Object.prototype 是原型链的终结，Object.prototype 的**`__proto__`**是 null
