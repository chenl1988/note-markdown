## class

- class 声明会提升，但不会初始化赋值。

```
const foo = new foo(); //foo is not defined
class Foo {
  constructor() {
    this.foo = 42;
  }
}
```

- class 内部分启用严格模式
- class 的所有方法（包括静态方法和实例方法）都是不可枚举的
- class 的所有方法（包括静态方法和实例方法）都没原型对象 prototype，所以也没有[[construct]]，不能使用 new 来调用

```
class Foo1 {
  constructor() {
    this.foo = 42;
  }
  print() {
    console.log(this.foo);
  }
}
const foo1 = new Foo1();
const fooPrint = new foo1.print(); //foo1.print is not a constructor
```

- 必须使用 new 调用 class
- class 内部无法重写类名
