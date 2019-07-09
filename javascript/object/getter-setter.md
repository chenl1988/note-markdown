## getter 与 setter

- getter 和 setter 是 ES5 提供的新特性
- 一个 getter 是一个获取某个特定属性的值的方法
- 一个 setter 是一个设置某个属性的值的方法
- 可以为预定义的或用户定义的对象定义 getter 和 setter 以支持新增的属性
- 定义 getter 和 setter 的语法采用对象字面量的语法
  - getter 方法是必须是无参数的
  - setter 方法只接受一个参数（设置为新值）

```
var dreamapple = {
  firstName: 'dream',
  lastName: 'apple',
  get fullName() {
    return this.firstName + " " + this.lastName;
  },
  set fullName(fullName) {
    var names = fullName.trim().split(' ');
    if (2 === names.length) {
      this.firstName = names[0];
      this.lastName = names[1];
    }
  }
}

dreamapple.firstName = "Dream";
dreamapple.lastName = "Apple";
console.log(dreamapple.fullName); //getter

dreamapple.fullName = "Jams King"; //setter
console.log(dreamapple.firstName);
console.log(dreamapple.lastName);
```
