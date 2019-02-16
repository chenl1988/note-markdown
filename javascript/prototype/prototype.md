## prototype

- prototype是一个显式的原型属性
- 每个函数创建的时候都会默认创建一个prototype属性
- prototype属性的值是一个对象，其中只有一个 constructor（构造函数）属性，其中存放的是函数本身
---
- Object.prototype这个对象是引擎自己创建的
- Function.prototype也是引擎创建的，并且通过__proto__将两者联系起来（即`Function.prototype.__proto__.constructor: function Object()`）
- 先有了Function.prototype才有的function Function()
- Object.prototype是原型链的终结，Object.prototype的__proto__是null






