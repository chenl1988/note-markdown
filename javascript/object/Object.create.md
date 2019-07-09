## Object.create

- 该方法非常有用，因为它允许你为创建的对象选择其原型对象，而不用定义一个构造函数

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
