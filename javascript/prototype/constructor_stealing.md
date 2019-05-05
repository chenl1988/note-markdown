## 借用构造函数（constructor stealing）

- 也叫经典继承，基本思想：即在子类的构造函数中调用超类的构造函数

```
function Father(){
  this.color = ['red','green','blue'];
}
function Son(){
  Father.call(this); //继承了Father，具向父类传递传参数
}

var instance1 = new Son();
instance1.color.push('black');
console.log(instance1.color);

var instance2 = new Son();
console.log(instance2.color);//"red,blue,green" 可见引用类型值是独立的
```

- 借用构造函数解决了原型链的两大问题：
  - 保证了原型链中引用类型值的独立，不再被所有实例共享
  - 子类型创建时也能够向父类中传递参数

## 借用构造函数存在的问题

- 方法都在构造函数中定义，因此函数不能被复用
- 而且父类中定义的方法对子类也是不可见的
- 由于以上两个问题，借用构造函数很少单独使用
