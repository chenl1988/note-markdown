## Object.create

- 该方法非常有用，因为它允许你为创建的对象选择其原型对象，而不用定义一个构造函数
- Object.create()方法创建一个新对象，使用现有的对象来提供新创建的对象的__proto__。 

- 语法：Object.create(proto[, propertiesObject])
  - proto：新创建对象的原型对象。
  - propertiesObject：可选，如果没有指定为undefined、对象的属性描述符以及相应的属性名称

```
var Animal = {
  type: "Invertebrates",
  displayType: function () {
    console.log(this.type);
  }
}

var animal1 = Object.create(Animal);
animal1.displayType();

var fish = Object.create(Animal);
fish.type = "Fishes";
fish.displayType();
```
