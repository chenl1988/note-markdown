## prototype

- prototype 是一个显式的原型属性

- 每一个JavaScript对象(null除外)在创建的时候就会与之关联另一个对象，这个对象就是我们所说的原型，每一个对象都会从原型"继承"属性。

- 每个函数创建的时候都会默认创建一个 prototype 属性，prototype 属性指向函数的原型对象，这个对象正是调用该构造函数页创建的实例的原型

- 只有函数对象才拥有 prototype 属性

- prototype 对象上的所有属性和方法，都会被构造函数的实例继承，这意味着，可以把那些不变的属性和方法，直接定义在 prototype 对象上

- prototype 属性的值是一个对象，其中有 constructor（构造函数）和`__proto__`属性

  - constructor 解决了对象识别问题，即可以通过该属性判断出实例是哪个构造函数创建的
  
  - `__proto__` 每个实例都有一个`__proto__`属性，指向构造函数的原型对象，构造函数的原型对象它本身也一个实例，所以它的内部会有一个`__proto__`属性

- 使用原型（prototype）的好处是可以让所有对象实例共享它所包含的属性和方法

---

- Object.prototype 这个对象是引擎自己创建的
- Function.prototype 也是引擎创建的，并且通过**proto**将两者联系起来（即`Function.prototype.__proto__.constructor: function Object()`）
- 先有了 Function.prototype 才有的 function Function()
- Object.prototype 是原型链的终结，Object.prototype 的**`__proto__`**是 null

---

## Prototype 模式的验证方法

- isPrototypeOf()：判断 prototype 对象和某个实例之间的关系:`Cat.prototype.isPrototypeOf(cat1)`
- hasOwnProperty()：每个实例对象都有一个 hasOwnProperty()方法，用来判断某一个属性是本地属性还是继承自 prototype 对象的属性：`cat1.hasOwnProperty("name")`;
- in 运算符: 可以用来判断，某个实例是否包含某个属性，不管是不是本地属性`"name" in cat1`; in 运算符还可以用来遍历某个对象的所有属性
