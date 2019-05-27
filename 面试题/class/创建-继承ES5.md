```
/*
 * 类的创建（es5）：new一个function，在这个function的prototype里面增加属性和方法。
 */

function Animal(name) {
  //属性
  this.name = name || "Animal";
  //实例方法
  this.sleep = function () {
    console.log(this.name + "正在睡觉");
  }
}

//原型方法
Animal.prototype.eat = function (food) {
  console.log(this.name + "正在吃" + food);
}

/*
 * 类的继承---原型链继承
 * 特点：基于原型链，既是父类实例，也是子类实例
 * 缺点：无法实现多继承
 */

function Cat_1() {}
//new了一个空对象,这个空对象指向Animal并且Cat.prototype指向了这个空对象，这种就是基于原型链的继承
Cat_1.prototype = new Animal();
Cat_1.prototype.name = "cat";

//Test Code
var cat_1 = new Cat_1();
console.log(cat_1.name);
console.log(cat_1.eat('fish'));
console.log(cat_1.sleep());
console.log(cat_1 instanceof Animal); //true
console.log(cat_1 instanceof Cat_1); //true

console.log("-----------------------------");
/*
 * 类的继承---构造继承 (使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类【没用到原型】)
 * 特点：可以实现多继承
 * 缺点：只能继承父类实例的属性和方法，不能继承原型上的属性和方法
 */
function Cat_2(name) {
  Animal.call(this);
  this.name = name || 'Tom';
}
// Test Code
var cat_2 = new Cat_2();
console.log(cat_2.name);
console.log(cat_2.sleep());
console.log(cat_2 instanceof Animal); //false
console.log(cat_2 instanceof Cat_2); //true

console.log("-----------------------------");
/*
 * 类的继承---组合继承 （相当于构造继承和原型链继承的组合体。通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用）
 * 特点：可以继承实例属性/方法，也可以继承原型属性/方法
 * 缺点：调用了两次父类构造函数，生成了两份实例
 */
function Cat_3(name) {
  Animal.call(this);
  this.name = name || 'Tom';
}
Cat_3.prototype = new Animal();
Cat_3.prototype.constructor = Cat_3();

// Test Code
var cat_3 = new Cat_3();
console.log(cat_3.name);
console.log(cat_3.sleep());
console.log(cat_3 instanceof Animal); //true
console.log(cat_3 instanceof Cat_3); //true


console.log("-----------------------------");
/*
 * 类的继承---寄生组合继承 （通过寄生方式，砍掉父类的实例属性，这样，在调用两次父类的构造的时候，就不会初始化再次实例方法/属性）
 * 较为推荐
 */
function Cat_4(name) {
  Animal.call(this);
  this.name = name || 'Tom';
}
(function () {
  //创建一个没有实例方法的类
  var Super = function () {};
  Super.prototype = Animal.prototype;
  //将实例作为子类原型
  Cat_4.prototype = new Super();
})();

// Test Code
var cat_4 = new Cat_4();
console.log(cat_4.name);
console.log(cat_4.sleep());
console.log(cat_4 instanceof Animal); //true
console.log(cat_4 instanceof Cat_4); //true
```
